# ScenarioContext

You may have at least seen the ScenarioContext from the code that SpecFlow generates when a missing step definition is found: `ScenarioContext.Pending();`

`ScenarioContext` provides access to several functions, which are demonstrated using the following scenarios.

## Accessing the ScenarioContext

### in Bindings

To access the `ScenarioContext` you have to get it via [context injection](Context-Injection.md).

Example: 

```
[Binding]
public class Binding
{
	private ScenarioContext _scenarioContext;

    public Binding(ScenarioContext scenarioContext)
    {
		_scenarioContext = scenarioContext;
    }
}

```

Now you can access the `ScenarioContext in all your Bindings with the `_scenarioContext` field.

### in Hooks

#### Before/AfterTestRun

Accessing the `ScenarioContext` is not possible, as no `Scenario` is executed when the hook is called.

#### Before/AfterFeature

Accessing the `ScenarioContext` is not possible, as no `Scenario` is executed when the hook is called.

#### Before/AfterScenario

Accessing the `ScenarioContext` is done like in [normal bindings](#in-Bindings)

#### Before/AfterStep

Accessing the `ScenarioContext` is done like in [normal bindings](#in-Bindings)



## ScenarioContext.Pending

This is the default behavior for a missing step definition, but you can also use it directly if (**why?**) you want to:

in the .feature:

        Scenario: Pending step
	    When I set the ScenarioContext.Current to pending
	    Then this step will not even be executed

and the step definition:

        [When("I set the ScenarioContext.Current to pending")]
        public void WhenIHaveAPendingStep()
        {
            ScenarioContext.Pending();
        }

        [Then("this step will not even be executed")]
        public void ThisStepWillNotBeExecuted()
        {
            throw new Exception("See!? This wasn't even thrown");
        }




## Storing data in the ScenarioContext

ScenarioContext helps you store values in a dictionary between steps. This helps you to organize your step definitions better than using private variables in step definition classes.

There are some type-safe extension methods that help you to manage the contents of the dictionary in a safer way. To do so, you need to include the namespace TechTalk.SpecFlow.Assist, since these methods are extension methods of ScenarioContext.

## ScenarioContext.ScenarioInfo

`ScenarioContext.ScenarioInfo` allows  you to access information about the scenario currently being executed, such as its title and tags:

In the .feature file:

``` gherkin
    @showUpInScenarioInfo @andThisToo
    
    Scenario: Showing information of the scenario
	
    When I execute any scenario
	Then the ScenarioInfo contains the following information
		| Field | Value                               |
		| Tags  | showUpInScenarioInfo, andThisToo    |
		| Title | Showing information of the scenario |
```

and in the step definition:

``` csharp
        private class ScenarioInformation
        {
            public string Title { get; set; }
            public string[] Tags { get; set; }
        }

        [When(@"I execute any scenario")]
        public void ExecuteAnyScenario(){}

        [Then(@"the ScenarioInfo contains the following information")]
        public void ScenarioInfoContainsInterestingInformation(Table table)
        {
            // Create our small DTO for the info from the step
            var fromStep = table.CreateInstance<ScenarioInformation>();
            fromStep.Tags =  table.Rows[0]["Value"].Split(',');

            // Short-hand to the scenarioInfo
            var si = _scenarioContext.ScenarioInfo;

            // Assertions
            si.Title.Should().Equal(fromStep.Title);
            for (var i = 0; i < si.Tags.Length -1; i++)
            {
                si.Tags[i].Should().Equal(fromStep.Tags[i]);
            }
        }
```

Another use is to check if an error has occurred, which is possible with the `ScenarioContext.TestError` property, which simply returns the exception.

You can use this information for “error handling”. Here is an uninteresting example:

in the .feature file:

``` gherkin
         #This is not so easy to write a scenario for but I've created an AfterScenario-hook
         @showingErrorHandling 
         Scenario: Display error information in AfterScenario
	    When an error occurs in a step

```

and the step definition:

``` csharp
        [When("an error occurs in a step")]
        public void AnErrorOccurs()
        {
            "not correct".Should().Equal("correct");
        }

        [AfterScenario("showingErrorHandling")]
        public void AfterScenarioHook()
        {
            if(_scenarioContext.TestError != null)
            {
                var error = _scenarioContext.TestError;
                Console.WriteLine("An error ocurred:" + error.Message);
                Console.WriteLine("It was of type:" + error.GetType().Name);
            }
        }
```

This is another example, that might be more useful:

``` csharp
       [AfterScenario]
       public void AfterScenario()
        {
            if(_scenarioContext.TestError != null)
            {
                WebBrowser.Driver.CaptureScreenShot(_scenarioContext.ScenarioInfo.Title);
            }
        }
```

In this case, MvcContrib is used to capture a screenshot of the failing test and name the screenshot after the title of the scenario.


## ScenarioContext.CurrentScenarioBlock

Use `ScenarioContext.CurrentScenarioBlock` to query the “type” of step (Given, When or Then). This can be used to execute additional setup/cleanup code right before or after Given, When or Then blocks.

in the .feature file:

``` gherkin
        Scenario: Show the type of step we're currently on
	     Given I have a Given step
		  And I have another Given step
	     When I have a When step
	     Then I have a Then step
```

and the step definition:

``` csharp
        [Given("I have a (.*) step")]
        [Given("I have another (.*) step")]
        [When("I have a (.*) step")]
        [Then("I have a (.*) step")]
        public void ReportStepTypeName(string expectedStepType)
        {
            var stepType = _scenarioContext.CurrentScenarioBlock.ToString();
            stepType.Should().Equal(expectedStepType);
        }
```

## ScenarioContext.StepContext

Sometimes you need to access the currently executed step, e.g. to improve tracing. Use the `_scenarioContext.StepContext` property for this purpose.