---
title:  "Coding Tip: Errors are NOT Always Bad"
description: "Thoughts on how to better deal with error prone areas in code"
date: 30-July-2019
---

One of the traits of a good programmer is to properly handle error prone scenarios in code. For example, If a file doesn't exist in the filesystem, catch the exception/error and show a friendly message to the end user or if you want to access a value in a dictionary/map, check first to see if its related key is there before accessing it or silently handle it if the key doesn't exist. These types of error handling saves you from lots of bad looking errors and showstoppers that your end users may face and most of the time it's a good thing.

But, there will be some scenarios where its better for these errors to be popped up instead of silently ignoring them. In a project that I am involved, we faced a huge data issue just because an bug was silently ignored. The scenario was that in a sub-process we were generating a dynamic dictionary based on received data and feeding that data back to another sub-process. For those who have worked with Python, knows that <span>`dict.get('some_key')`</span> and <span>`dict['some_key']`</span> both does the same thing and it's to get the value for the key: <span>`some_key`</span>. The only difference is that if the key doesn't exist in the dictionary, the former one returns <span>`None`</span> or <span>`Null`</span> without any error and the latter one throws an exception/error/traceback.

In my experience, what I have seen some developers doing is trying to be on the safe side (which from their perspective is avoiding traceback/error) and always using handy methods such as <span>`dict.get('some_key')`</span>, which shouldn't be the case. Scenarios should be analyzed, questions like is it fine to assume and pass <span>`None`</span> or <span>`Null`</span> to the next function if the key doesn't exist? Is the existence of the <span>`some_key`</span> in <span>`dict`</span> a must, as it may be passed to a payroll related function and assuming any value other than the one expected may affect calculations badly? Considering the latter scenario, it's better to use <span>`dict['some_key']`</span> and take the risk of having a bad looking traceback/error in the system instead of having wrong payroll calculations. 

## Conclusion

We have to be a lot cautious with little details like this. In our case, it was a lot safer for us to use <span>`dict['some_key']`</span> (which throws an error if they key doesn't exist in a dictionary) cause there was no way for our app to move forward silently until the <span>`some_key`</span> key wasn't present in the <span>`dict`</span> dictionary. It was totally worth it to have a traceback instead of wrong calculations :).