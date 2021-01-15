---
layout: post
title:  "Simplify 'If/Else' in Javascript"
date:   2020-02-17 18:05:55 +0300
image:  '/assets/img/language/js-logo.png'
tags:   [javascript,coding,web programming,tech]
---

When developing in Javascript, we usually use if/else statement to solve simple conditional logic. The statement executes a block of code if a specified condition is true. If the condition is false, another block of code can be executed. That's what we already know right !!! What will happen if we encounter the situation of complex conditional logic like below:

{% highlight javascript %}
const buttonClick = (status)=>{
  if(status == 1){
    doFunc1('home')
    doFunc2('homePage')
  }else if(status == 2){
    doFunc1('about')
    doFunc2('aboutPage')
  }else if(status == 3){
    doFunc1('archived')
    doFunc2('archivedPage')
  }else if(status == 4){
    doFunc1('success')
    doFunc2('SuccessPage')
  }else if(status == 5){
    doFunc1('cancel')
    doFunc2('CancelPage')
  }else {
    doFunc1('other')
    doFunc2('IndexPage')
  }
}
{% endhighlight %}

<br/>
The above code simply create a nested If/else statement to do two things (doFunc1 and doFunc2) based on the condition in the IF(or ELSE IF) line. It would be troublesome to maintain such lines of code like this. Instead, normally people will try to use the **switch** statement.

{% highlight javascript %}
const buttonClick = (status)=>{
  switch (status){
    case 1:
      doFunc1('home')
      doFunc2('HomePage')
      break
    case 2:
      doFunc1('about')
      doFunc2('AboutPage')
      break
    case 3:
      doFunc1('archived')
      doFunc2('ArchivedPage')
      break  
    case 4:
      doFunc1('success')
      doFunc2('SuccessPage')
      break
    case 5:
      doFunc1('cancel')
      doFunc2('CancelPage')
      break
    default:
      doFunc1('other')
      doFunc2('IndexPage')
      break
  }
}
{% endhighlight %}

<br/>
Using the switch statement will make your code look cleaner. If some logic in the cases are similar, we can group them up by combining cases (without using the **break** line).

{% highlight javascript %}
....
case 2:
case 3:
  doFunc1('archived')
  doFunc2('archivedPage')
  break  
....
{% endhighlight %}

<br/>
Surely the switch statement makes our code look much cleaner than using if/else
.But there is a simpler way to write it

{% highlight javascript %}
const actions = {
  '1': ['home','HomePage'],
  '2': ['about','AboutPage'],
  '3': ['archived','ArchivedPage'],
  '4': ['success','SuccessPage'],
  '5': ['cancel','CancelPage'],
  'default': ['other','IndexPage'],
}

const onButtonClick = (status)=>{
  let action = actions[status] || actions['default'],
      logName = action[0],
      pageName = action[1]
  doFunc1(logName)
  doFunc2(pageName)
}
{% endhighlight %}

<br/>
The above modified code looks cleaner and still serve out purpose. We transform the switch statement into a JSON object containing all the options.<br/>
When the 'onButtonClick' function is triggered, we pull out the matched 'status' from the element inside the 'action' object and pass to other functions.

<br/>
Another way to is to use Map instead of Object, we can modify the above code as below:

{% highlight javascript %}
const actions = new Map([
  [1, ['home','HomePage']],
  [2, ['about','AboutPage']],
  [3, ['archived','ArchivedPage']],
  [4, ['success','SuccessPage']],
  [5, ['cancel','CancelPage']],
  ['default': ['other','IndexPage']],
])

const onButtonClick = (status)=>{
  let action = actions.get(status) || actions.get('default')
  doFunc1(action[0])
  doFunc2(action[1])
}
{% endhighlight %}

Why we use Map ? There are many advantages:

* A Map's key can be any value, meanwhile object can only accept String or symbols.
* We can easily get the number of key-value pairs by using 'size' attribute. We can still do so with Object but it requires additional step.