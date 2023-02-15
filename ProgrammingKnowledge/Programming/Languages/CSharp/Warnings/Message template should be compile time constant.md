
From [Stackoverflow](https://stackoverflow.com/questions/65874828/message-template-should-be-compile-time-constant):

> The answer is that string interpolation prevents structured logging. When you pass the variables after the message, you make it possible for the logger to save them separately. If you just save the log to a file you may not see a difference, but if you later decide to log to a database or in some JSON format, you can just change your logging sink and you will be able to search through the logs much easier without changing all the log statements in your code.

#Rider
#Warnings
#CSharp 