COTTaskHelper
=============

A thin wrapper around NSTask that provides block callbacks for task completion, error, and output.

````Objective-C
NSTask *task = [[NSTask alloc] init];
[task setLaunchPath:@"/bin/bash"];
[task setArguments:@[@"-c", @"some command"]];

COTTaskHelper *taskHelper = [[COTTaskHelper alloc] init];
taskHelper.task = task;
taskHelper.outputHandler = ^(NSData *outputData) {
  NSString *outputString = [[NSString alloc] initWithData:outputData encoding:NSASCIIStringEncoding];
  NSLog(@"%@", outputString);
};
taskHelper.completionHandler = ^{
  NSLog(@"Task complete!");
};
taskHelper.errorHandler = ^(NSData *errorData) {
  NSString *errorString = [[NSString alloc] initWithData:errorData encoding:NSASCIIStringEncoding];
  NSLog(@"%@", errorString);
};

[taskHelper launch];
````
