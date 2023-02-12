# Lift Up Conditional

## TLDR 


Verwende es um komplexe `if`-statements zu vereinfachen. Siehe dazu  [Gilded Rose](http://gregorriegler.com/2019/12/08/lift-up-conditional.html) .


> The lift up conditional refactoring is useful for complex and deeply nested conditionals, where related parts are scattered all over the place. I am using the Gilded Rose Kata, which is a perfect example, as it consists of a really complex conditional.

<iframe width="560" height="315" src="https://www.youtube.com/embed/0bhfWtZocF8" frameborder="0" allowfullscreen=""></iframe>

[the code on my GitHub](https://github.com/gregorriegler/GildedRose-Refactoring-Kata/tree/lift-up-if-refactoring/Java) 

Gibt auch nen brauchbaren Blog von Emily Bach, hier der [Link](https://coding-is-like-cooking.info/tag/code-coverage/) 


---

## Guter Artikel


### **No more long, complex conditional statements**


![](https://miro.medium.com/max/1400/1*JkWWNkgvFpSBP_u-gh01xw.jpeg)

### **A Common Problem**

As a developer, at some point you’ve probably had to deal with line after line of seemingly never-ending code written by some prodigious mind and dating back to circa 3 B.C.

You’ve dealt with functions that come out of nowhere, variables with unspeakable names, methods that call to methods that call to methods… In short, what one might call a real gem.

The thing is, that code works just fine and the company that pays you would like it to keep working. And you probably want the company to keep paying you each month, so here’s a friendly tip: choose your next move wisely.

While looking through the code, something catches your eye in the chaos before you. It’s a conditional statement, a good old _If/else_ except for one difference: it would appear to last forever. It links one condition to another as if there were no tomorrow, an _if_ within an _else_ within another _if_ that has another _elseIf_ and so on and so forth to the point that you bow your head and ask yourself two fundamental questions:

Firstly, what was the initial condition I wanted to check? And secondly, and more importantly, why didn’t I listen to my Mom and study medicine?

![](https://miro.medium.com/max/1400/1*TFHKCBevI6Eu99CimWgE_Q.jpeg)

### **Lift-Up Conditional: The Ultimate Solution**

So, if you’ve ever found yourself in a situation like this, don’t fret. I have some good news for you: there’s a solution!

The technique I want to tell you about today is called **lift-up conditional**. In essence, it lets you manipulate complex conditional statements to group together all the statements that refer to a specific condition.

The idea is to break up the code and then group all the logic that makes reference to a specific condition in the same part of the code, thus preventing conditions from getting mixed up. The result is much cleaner code that any developer can read.

To do this, you just need to follow a few simple steps:

1.  Identify the condition you want to use the technique on.
2.  Extract ALL the code that makes up the monstrous _if/else_ to a new method. Let’s call it “temporary method.”
3.  Create a new _if/else_ with the condition you selected in step one.
4.  Introduce the temporary method in both the _if_ and _else_ you just created.
5.  Execute an inline for the temporal method so that it disappears and you’re left with a copy of the code in both parts of the _if/else._
6.  Now just add _true_ or _false_ to all the conditions in the code by comparing them to the condition you initially chose.
7.  All that’s left to do is simplify the redundant expressions that arise from the process.

At this point, you’re probably thinking, “that doesn’t sound so simple. I got lost at step 5.” I don’t blame you. But be patient because I still haven’t introduced you to today’s special guest.

Following the steps above would be far more complicated without the right tools. This technique assumes you’re using the IDE IntelliJ.

Thanks to the many automated refactors it offers, this IDE will lighten your load and make you feel like a wizard at your keyboard. Combine this key with that one, select the option to simplify as proposed by the IDE, hit enter and… BOOM! One less line of useless code.

> You, your code, a good refactor technique, maybe some candles… Just something to think about…

Careful, though! Don’t give in to temptation and start simplifying code without checking that it still functions after every little change you make. What you definitely don’t want is for your code to stop working and not know exactly where you screwed up.

Be sure you don’t deviate from your main goal, which is to clean up the code and make it more compact but leave it functioning like it always has.

Check out this example by [Emily Baches](https://twitter.com/emilybache?lang=es), who was the first to use this technique and was kind enough to share it with the community, you can see how to apply it step by step.

### In Conclusion

Knowing how to take full advantage of the tools available should represent a basic skill for any developer.

This example shows just how important it is to follow a certain structure when refactoring code. By making the most of the automated functions your IDE has to offer, it’s easy to optimize your work and leave a better legacy for the next developer to face that code.

#Refactoring
