Welcome to SpecFlow's documentation!
====================================

SpecFlow is a test automation solution for .NET built upon the BDD paradigm, and part of the `Cucumber <http://cucumber.io/>`_ family. Use SpecFlow to define, manage and automatically execute human-readable acceptance tests in .NET projects (Full Framework and .NET Core).

SpecFlow tests are written using `Gherkin <https://cucumber.io/docs/gherkin/>`_, which allows you to write test cases using natural languages. SpecFlow uses the official Gherkin parser, which supports over 70 languages. These tests are then tied to your application code using so-called :doc:`bindings <Bindings/Bindings>`, allowing you to execute the tests using the testing framework of your choice. You can also execute your tests using SpecFlow's own dedicated test runner, SpecFlow+ Runner.

SpecFlow consists of several components:

* SpecFlow (open source): This is the core of SpecFlow, providing the functions for binding Gherkin feature files 
* `SpecFlow+ Runner <https://specflow.org/plus/documentation/SpecFlowPlus-Runner/>`_ (closed source): This is SpecFlow's dedicated test runner, and provides additional features such as `advanced execution options <https://specflow.org/plus/documentation/Execution/>`_ and `execution reports <https://specflow.org/plus/documentation/Reports/>`_ (HTML, XML, JSON). SpecFlow+ Runner is free of charge, and only requires a `SpecFlow Account <https://specflow.org/2020/introducing-the-specflow-account/>`_.
* `SpecFlow+ LivingDoc <https://specflow.org/plus/documentation/SpecFlowPlus-LivingDoc/>`_ (closed source): LivingDoc is an extension for Azure DevOps/TFS that takes your Gherkin feature files and renders them in an easily readable format with syntax highlighting. You can view the output directly in Azure DevOps/TFS, meaning that anyone with access to the system can easily review your specifications when needed. SpecFlow+ LivingDoc is free of charge, and only requires a `SpecFlow Account <https://specflow.org/2020/introducing-the-specflow-account/>`_.

SpecFlow also includes a `Visual Studio extension <Tools/Visual-Studio-Integration>`_ that adds a number of helpful features to Visual Studio (e.g. Intellisense, feature file templates, context menu entries). However, SpecFlow is not tied to Visual Studio; you can use SpecFlow with Mono or VSCode, for example.

Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`

.. toctree::
   :maxdepth: 1
   :caption: Installation
   :hidden:

   Installation/Requirements.md
   Installation/Installation.md 
   Installation/Install-IDE-Integration.md
   Installation/NuGet-Packages.md
   Installation/Project-and-Item-Templates.md
   Installation/Troubleshooting-Visual-Studio-Integration.md
   Installation/.NET-Support.md
   Installation/Unit-Test-Providers.md
   Installation/SpecFlow-and-.NET-Core.md
   Installation/Breaking-Changes-with-SpecFlow-3.0.md


.. toctree::
   :maxdepth: 1
   :caption: Configuration
   :hidden:

   Configuration/Configuration.md

.. toctree::
   :maxdepth: 1
   :caption: Bindings
   :hidden:

   Bindings/Bindings.md
   Bindings/Step-Definitions.md
   Bindings/Scoped-Step-Definitions.md
   Bindings/Asynchronous-Bindings.md

   Bindings/Hooks.md

   Bindings/Sharing-Data-between-Bindings.md
   Bindings/Context-Injection.md
   Bindings/ScenarioContext.md
   Bindings/FeatureContext.md
   Bindings/Calling-Steps-from-Step-Definitions.md

   Bindings/Step-Argument-Transformations.md
   Bindings/Step-Argument-Conversions.md

   Bindings/Use-Bindings-from-External-Assemblies.md

   Bindings/Renaming-Steps.md
   Bindings/SpecFlow-Assist-Helpers.md
   Bindings/FSharp-Support.md

.. toctree::
   :maxdepth: 1
   :caption: Gherkin
   :hidden:

   Gherkin/Using-Gherkin-Language-in-SpecFlow.md
   Gherkin/Feature-Language.md

.. toctree::
   :maxdepth: 1
   :caption: Execution
   :hidden:

   Execution/Executing-SpecFlow-Scenarios.md
   Execution/Test-Results.md
   Execution/Parallel-Execution.md
   Execution/Debugging.md

.. toctree::
   :maxdepth: 1
   :caption: Tools
   :hidden:

   Tools/Tools.md
   Tools/Generate-Tests-From-MsBuild.md
   Tools/Visual-Studio-Integration.md
   Tools/Visual-Studio-Integration-Editing-Features.md
   Tools/Visual-Studio-Integration-Navigation-Features.md
   Tools/Visual-Studio-Test-Explorer-Support.md
   Tools/Generating-Skeleton-Code.md
   Tools/Cucumber-Messages.md
   Tools/Reporting.md

.. toctree::
   :maxdepth: 1
   :caption: Integrations
   :hidden:

   Integrations/MsTest.md
   Integrations/SpecFlow+Runner-Integration.md
   Integrations/Azure-DevOps.md
   Integrations/Teamcity-Integration.md
   Integrations/Browserstack.md
   Integrations/CodedUI.md

.. toctree::
   :maxdepth: 1
   :caption: Enhance SpecFlow
   :hidden:

   Enhance/Value-Retriever.md
   Enhance/Plugins.md
   Enhance/Plugins-(Legacy).md
   Enhance/Available-Plugins.md
   Enhance/Available-Containers-&-Registrations.md

.. toctree::
   :maxdepth: 1
   :caption: Common Issues
   :hidden:

   CommonIssues/Troubleshooting.md
   CommonIssues/Known-Issues.md

.. toctree::
   :maxdepth: 1
   :caption: Developing on SpecFlow
   :hidden:

   DevelopingOnSpecFlow/Prerequisite.md
   DevelopingOnSpecFlow/LocalSetup.md
   DevelopingOnSpecFlow/Definition-of-Terms.md
   DevelopingOnSpecFlow/Projects.md
   DevelopingOnSpecFlow/SpecialFiles.md
   DevelopingOnSpecFlow/potentialProblems.md
   DevelopingOnSpecFlow/Coding-Style.md

.. toctree::
   :maxdepth: 1
   :caption: Miscellenious
   :hidden:

   Misc/Usage-Analytics.md