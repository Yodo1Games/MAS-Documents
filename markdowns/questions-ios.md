# iOS Questions

## What is the primary cause of errors during compilation?

The cause is most likely a dependency conflict. MAS includes several third party libraries, and you will need to remove duplicates of these libraries elsewhere in your code base. 

## How can pubs address “MAX Integration Incomplete” issue when they upload their app to App store?

![](./../resource/applovin-max-debugger.png)

This pop-up window is from applovin, which will stop appearing by deleting `NSAllowsArbitraryLoadsInWebContent` from Info.plist. 

