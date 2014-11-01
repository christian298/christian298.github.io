---
layout: post
title:  "NSURLSession"
date:   2014-05-11 16:04
category: ios
---

First create a NSURLRequest. For this you need a NSURL object which is passed to the NSURL class methode requestWithURL:
{% highlight objc %} 
	NSURL *url = [NSURL URLWithString:@"http://www.google.com"];
    NSURLRequest *request = [NSURLRequest requestWithURL:url];
{% endhighlight %}

Then create a NSURLSession and a task for the request.

{% highlight objc %} 
    NSURL *url = [NSURL URLWithString:@"http://www.google.com"];
    NSURLRequest *request = [NSURLRequest requestWithURL:url];
    
    NSURLSession *session = [NSURLSession sharedSession];
    NSURLSessionDataTask *task = [session dataTaskWithRequest:request 
    	completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
        	NSLog(@"length: %lu", [data length]);
	        if (error == nil) {
	            NSString *content = [[NSString alloc] initWithData:data 
	            	encoding:NSUTF8StringEncoding];
	            NSLog(@"%@", content);
	        }
    }];
    [task resume];
{% endhighlight %}