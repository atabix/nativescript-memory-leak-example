# NativeScript Memory Leak Example
This repository serves to provide a reproduceable memory leak that occurs when navigating to another page.
In this example we navigate with a 1 second timeout to the same page in an endless loop.

## Use Case #1
Run the app with all of the same dependencies with one exception:
@nativescript/ios@6.5.4

Allow the app to run for a period of thirty minutes.

## Use Case #2
Run the app with all of the same dependencies with one exception:
@nativescript/ios@7.2.0

Allow the app to run for a period of thirty minutes.

## Results
The app starts around ~74MB in both uses cases. In this first couple of minutes the app slowly increases in total memory used, incrementing about 1MB every couple of seconds.

After this initial period the memory seems to stabilize at around 93MB.

The same test has been applied to two very different apps in production with pages that are more complex. This example here resulted in 1MB increments. The production apps resulted in 50MB increments. In combination with navigating between different kinds of pages this memory problem is compounded, eventually resulting in the app shutting itself down.

This behavior remained consistent when manually calling `Utils.GC()` and using `clearHistory: true` on navigation.
