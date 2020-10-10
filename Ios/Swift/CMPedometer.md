## Conception  
An object for fetching the system-generated live walking data.  
  
## When use  
1. to retrieve step counts and other information about the distance traveled  
and the number of floors ascended or descended.  
2. to manage a cache of historic data that you can query.  
3. to ask for live updates as the data is processed.  
  
## How to use  
  
  
### queryPedometerData(from:to:withHandler:)  
1. Method to retrieve data that has already been gathered.  
2. Method to retrieve historical pedestrian data between the specified dates.  
3. Only the past seven days worth of data is stored and available for you to retrieve.  

> Specifying a start date that is more than seven days in the past returns only the available data.  
  
### startUpdates(from:withHandler:)  
To get live updates, use this method to start the delivery of events to the handler you provide.  

1. Starts the delivery of recent pedestrian-related data to your app.  
2. The data passed to your handler block represents *the cumulative data*  
starting at the specified start date and ending at the current time.  
3. When the app is suspended, the delivery of updates stops temporarily.  
4. Upon returning to foreground or background execution, the pedometer object begins updates again.  
5. To stop the delivery of events, call the stopUpdates() method.  