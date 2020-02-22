---
layout: post
title:  "If/else burden in Javascript"
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

The above code simply create a nested If/else statement to do two things (doFunc1 and doFunc2) based on the condition in the IF(or ELSE IF) line. It would be troublesome to maintain such lines of code like this. Instead, normally people will try to use the 'switch' statement.

{% highlight javascript %}
const buttonClick = (status)=>{
  switch (status){
    case 1:
      doFunc1('home')
      doFunc2('homePage')
      break
    case 2:
      doFunc1('about')
      doFunc2('aboutPage')
      break
    case 3:
      doFunc1('archived')
      doFunc2('archivedPage')
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