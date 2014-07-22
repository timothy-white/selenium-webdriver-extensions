[![Build status](https://ci.appveyor.com/api/projects/status/xva7kjm1lyi3fqcu)](https://ci.appveyor.com/project/RaYell/selenium-helpers)

# Description
Extensions for Selenium WebDriver including jQuery selector support.

# Features
Some of the most important features of this library include:
* Generates jQuery selectors that can be used by Selenium WebDrivers to perform selections that CSS can't do
* Allows jQuery selectors to be used even on sites that don't use jQuery as it can load before performing a first search
* Very easy setup: install package with NuGet, include a namespace and start using it
* Supports all jQuery traversing methods for generation of complex selector chains
* Supports jQuery context switching
* High quality ensured by continous integration setup with Appveyor, unit and integration tests and 100% code coverage
* Well documented code following strict StyleCop and FxCop rules

# Installation
Run the following command in Visual Studio Packet Manager Console.
```posh
Install-Package Selenium.WebDriver.Extensions
```

# Usage

#### Include extensions
Include extensions namespace and set the derived `By` to be used.
```csharp
using Selenium.WebDriver.Extensions;
using By = Selenium.WebDriver.Extensions.By;
```

#### Basic example
Invoke jQuery selectors on the WebDriver.
```csharp
driver.FindElements(By.JQuerySelector("input:visible"))
```

#### Chaining
You can also chain jQuery traversing methods.
```csharp
var selector = By.JQuerySelector("div.myclass").Parents(".someClass").NextAll();
driver.FindElement(selector);
```

#### jQuery loading
If the site that you are testing with Selenium does not include jQuery this extension will automatically load the latest version when you run any of the `Find*` methods. If you want you can choose to load a different version of jQuery. The library used jQuery CDN by default, but if you want to use a completely different source, that's also supported

```csharp
driver.LoadJQuery("1.11.0"); // load specific version from default CDN
driver.LoadJQuery(new Uri("http://some.server/jquery.js")); // load a library from other source
```

#### jQuery variable name
When you create a jQuery selector using `By` helper class the resulting selector will use `jQuery` as library variable name. If you site is using a different variable name for this purpose you can pass this value as an optional parameter.

```csharp
var selector = By.JQuerySelector("div", jQueryVariable: "myJQuery");
```

#### jQuery context switch
You can use one `JQuerySelector` as a context of another `JQuerySelector`.

```csharp
var context = By.JQuerySelector("div.myClass");
var selector = By.JQuerySelector("ol li", context);
driver.FindElements(selector);
```