---
layout: default
title: Selenium WebDriver Extensions | selenium-webdriver-extensions | RaYell's GitHub
---

# Description
Extensions for Selenium WebDriver including jQuery and Sizzle selector support.

# Features
Some of the features of this library are:

* Generates jQuery and Sizzle selectors that can be used by Selenium WebDrivers to perform searches that CSS can't do
* Allows jQuery and Sizzle selectors to be used even on sites that don't use jQuery or Sizzle as it can load the library before performing a first search
* Very easy setup: install package with NuGet, include a namespace and start using it
* Supports jQuery traversing methods for generation of complex selector chains
* Supports jQuery and Sizzle context switching
* CI with Appveyor
* 100% code coverage with nUnit tests
* Well documented code following strict StyleCop and FxCop rules.

# Installation
Run the following command in Visual Studio Packet Manager Console.

{% highlight powershell %}
Install-Package Selenium.WebDriver.Extensions
{% endhighlight %}

# Documentation
API documentation can be found [here](https://rayell.github.io/selenium-webdriver-extensions/api).

# Usage

## Include extensions
Include extensions namespace and set the derived `By` to be used.

{% highlight csharp %}
using Selenium.WebDriver.Extensions;
using By = Selenium.WebDriver.Extensions.By;
{% endhighlight %}

## Basic jQuery example
Invoke jQuery selectors on the WebDriver.

{% highlight csharp %}
var driver = new ChromeDriver();
driver.FindElements(By.JQuerySelector("input:visible"))
{% endhighlight %}

## Chaining jQuery methods
You can also chain jQuery traversing methods.

{% highlight csharp %}
var driver = new ChromeDriver();
var selector = By.JQuerySelector("div.myclass").Parents(".someClass").NextAll();
driver.FindElement(selector);
{% endhighlight %}

## jQuery loading
If the site that you are testing with Selenium does not include jQuery this extension will automatically load the latest version when you run `FindElement` or `FindElements` method. If you want you can choose to load a different version of jQuery.

{% highlight csharp %}
var driver = new ChromeDriver();
driver.LoadJQuery("1.11.0");
{% endhighlight %}

## jQuery variable name
When you create a jQuery selector using `By` helper class the resulting selector will use `jQuery` as library variable name. If you site is using a different variable name for this purpose you can pass this value as an optional parameter.

{% highlight csharp %}
var driver = new ChromeDriver();
var selector = By.JQuerySelector("div", jQueryVariable: "myJQuery");
{% endhighlight %}

## jQuery context switch
You can use one `JQuerySelector` instance as a context of another `JQuerySelector`.

{% highlight csharp %}
var driver = new ChromeDriver();
var context = By.JQuerySelector("div.myClass");
var selector = By.JQuerySelector("ol li", context);
driver.FindElements(selector);
{% endhighlight %}

## Basic Sizzle example
Invoke Sizzle selectors on the WebDriver.

{% highlight csharp %}
var driver = new ChromeDriver();
driver.FindElements(By.SizzleSelector("input:visible"))
{% endhighlight %}

## Sizzle loading
If the site that you are testing with Selenium does not include Sizzle this extension will automatically load the latest version when you run `FindElement` or `FindElements` method. If you want you can choose to load a different version of jQuery.

{% highlight csharp %}
var driver = new ChromeDriver();
driver.LoadSizzle("1.11.1");
{% endhighlight %}

## Sizzle context switch
You can use one `SizzleSelector` instance as a context of another `SizzleSelector`.

{% highlight csharp %}
var driver = new ChromeDriver();
var context = By.SizzleSelector("div.myClass");
var selector = By.SizzleSelector("ol li", context);
driver.FindElements(selector);
{% endhighlight %}