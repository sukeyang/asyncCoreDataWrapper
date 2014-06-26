asyncCoreDataWrapper
====================

# access Core Data in multi thread by the easy way!

## First, prepare CoreData environment:

### 1. import CoreData Framework

![img1](http://ww4.sinaimg.cn/large/578b198bgw1ehrmzr0gwzj20rb059t98.jpg)

### 2. add xdatamodeld file and design your model and generate sub class file

![img2](http://ww2.sinaimg.cn/large/578b198bgw1ehrn492fm6j20ny0bb40f.jpg)

generate sub class in Editor > Create NSManagedContext SubClass

### 3. copy files to your project



### 4. init instance in appDelegate

```
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
    [[mmDAO instance] setupEnvModel:@"asyncCoreDataWrapper" DbFile:@"asyncCoreDataWrapper.sqlite"];
    return YES;
}


- (void)applicationWillTerminate:(UIApplication *)application
{
    // Saves changes in the application's managed object context before the application terminates.
    [self saveContext];
}

- (void)saveContext
{
    NSError *error = nil;
    if ([[mmDAO instance].bgObjectContext hasChanges]) {
        [[mmDAO instance].bgObjectContext save:&error];
    }
}
```

### 5. import catalog class in Prefix.pch file than you can use it anywhere

```
#import <Availability.h>

#ifndef __IPHONE_3_0
#warning "This project uses features only available in iOS SDK 3.0 and later."
#endif

#ifdef __OBJC__
    #import <UIKit/UIKit.h>
    #import <Foundation/Foundation.h>
    #import <CoreData/CoreData.h>
    #import "NSManagedObject+helper.h"
#endif

```


## How to use

### Create new object



