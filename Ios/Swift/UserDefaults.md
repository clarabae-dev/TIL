#### Conception  
Data dictionary like android SharedPreferences  

#### When to use
- Stores small amounts of user settings for as long as the app is installed.  
- Can save integers, booleans, strings, arrays, dictionaries, dates and more,  
but you should be careful not to save too much data  
because it will slow the launch of your app.  

#### Set Default Value  
```swift
UserDefaults.standard.register(defaults: [
        "SoundActive": true,
        "someOtherKey": "Some Message"
        ])
```
- default or fallback 용도로 활용  
