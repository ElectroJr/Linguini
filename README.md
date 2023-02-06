[![.NET](https://github.com/Ygg01/Linguini/actions/workflows/dotnet.yml/badge.svg?branch=master)](https://github.com/Ygg01/Linguini/actions/workflows/dotnet.yml)
![Nuget](https://img.shields.io/nuget/v/Linguini.Bundle?label=Linguini.Bundle)
![Nuget](https://img.shields.io/nuget/v/Linguini.Shared?label=Linguini.Shared)
![Nuget](https://img.shields.io/nuget/v/Linguini.Syntax?label=Linguini.Syntax)
![Nuget](https://img.shields.io/nuget/v/PluralRules.Generator?label=%20PluralRules.Generator)

# Linguini
Linguini is a C# implementation of Project Fluent, a localization system for natural-sounding translations with features like:

## Asymmetric Localization
Natural-sounding translations with genders and grammatical cases only when necessary. Expressiveness is not limited by the grammar of the source language.

## Progressive Enhancement
Translations are isolated; locale-specific logic doesn't leak to other locales. Authors can iteratively improve translations without impact on other languages.

## Modular
Linguini is highly modular. You only can use the parts you need.
Need just parsing? Get Linguni.Syntax.
Need only Plural Rules data? Get PluralRules.Generator and connect to XML CLDR Plural rules data.

## Performant
Linguini uses a zero-copy parser to parse the resources. While at the moment there are no benchmarks,
it is used by [RobustToolbox as](https://github.com/space-wizards/RobustToolbox) as a localization framework.

# How to get?

To install the [Fluent Bundle](https://www.nuget.org/packages/Linguini.Bundle/) type in your console:

```dotnet add package Linguini.Bundle```

You can also follow other NuGet installation instructions.

# How to use?

For a 1 minute tour of Linguini add this to your C# code:
```csharp
var bundler = LinguiniBuilder.Builder()
    .CultureInfo(new CultureInfo("en"))
    .AddResource("hello-user =  Hello, { $username }!")
    .UncheckedBuild();

var props = new Dictionary<string, IFluentType>()
{
    {"username", (FluentString)"Test"}
};

var message = bundler.GetAttrMessage("hello-user", props);
Assert.AreEqual("Hello, Test!", message);
```

## The 10 min tour - What do the lines mean?

Let's go line by line, and see how `LinguiniBuilder` works.

1. Init - Follwoing creates a `LinguiniBuilder` using a type-safe builder pattern.
    ```csharp
    var bundler = LinguiniBuilder.Builder()
    ```

2. Set the language - a translation bundle **must** have a language to translate to. In this case we choose English language.
    ```csharp
    .CultureInfo(new CultureInfo("en"))
    ```

3. Add a resource - translation bundle with no resources isn't really useful. We choose inline for easy of example, files are fine
    ```csharp
        .AddResource("hello-user =  Hello, { $username }!")
    ```

4. Complete the `ResourceBundle` - We call `UncheckedBuild()` to convert a builder to a bundle. Bundle will parse its resources and report
   errors. Since we don't care about errors, we are fine with `ResourceBundle` throwing errors.
   ```
       .UncheckedBuild();
   ```
   
5. Set p

# What is Fluent?
For more details see [Fluent syntax guide](https://projectfluent.org/fluent/guide/).

# Licenses

Linguini Bundle and associated projects are licensed under Apache and MIT licenses. Consult the LICENSE-MIT and LICENSE-APACHE for more detail.