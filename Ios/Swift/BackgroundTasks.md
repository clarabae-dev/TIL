#### Conception  
Use the BackgroundTasks framework to keep your app content up to date  
and run tasks requiring minutes to complete  
while your app is in the background.  

#### When to use  
- BGTaskScheduler  
A class for scheduling tasks run by submitting task requests  
that launch your app in the background.  
System can launch your app in the background to run tasks  
such as cleaning a database or updating the displayed data for an app  
when the device isn’t in use.  

#### How to use  
A task can run many times and requires:  
- Configuring the app to enable background task execution.  
- Registering a launch handler for the task.  
- Scheduling the task.  
