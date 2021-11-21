---
title: 'Finding elements frrom element - xpath paradox'
date: '2021-11-21T16:12:18+05:30'
toc: false
images:
tags:
  - testing
  - findElementsFromElement
  - nightwatch
  - xpath
  - selenium
  
---


## Xpath

Xpath is a locator strategy used to find elements on a page. XPath stands for XML path. XPath uses path expressions to select nodes from documents. Now working as a software developer has its advantages, one of them being, you work with cool digital devices.



## Usage In Automation Scripts

Xpath is a locator strategy used to find elements on a page. XPath stands for XML path. XPath uses path expressions to select nodes from documents.

## Finding Elements from Element

There are a lot of different approaches for this purpose in different frameworks. [Nightwatch](https://nightwatchjs.org) uses page objects to define elements under a section and Selenium provides methods to look for an target-element inside an element. So let's take an example of a simple page that looks like this.

```html
<div>
 <input/>
 <div id="container">
   <input id="input-username"/>
 </div> 
<div>
```
We need to find the inner input element using XPath. One of the simpler ways would be to use
`//input[id="input-username"]`  but what if the page looks like this.

```html
<div>
 <input/>
 <div id="container">
   <input id="input-username"/>
 </div> 
<div>
```
Selenium has functions like findElement from an element to suit this case.
```js
      // Get element with tag name 'div'
      let element = driver.findElement(By.css("div[id=container]"));

      // Get the element available with tag name 'input' inside element
      let inputElement = await element.findElements(By.css("input"));
```
You will get the inner input element as expected. But what if you decide to use xpath instead of css selector. 

```js
      // Get element with tag name 'div'
      let element = driver.findElement(By.css("div[id=container]"));

      // Get all the elements available on the page with tag name input
      let inputElement = await element.findElements(By.xpath("//input"));
```

It completely disregards that your code, to start searching for an element under a div element and gives you all the input element present on the page. Well xpath works differently it has different annotations for searching. In this example we are using `//` which means search anywhere for the element. There is useful website that discusses more such xpath expressions:  https://devhints.io/xpath. In this very example we need to use `./` for desired results.


Happy coding :smile:
