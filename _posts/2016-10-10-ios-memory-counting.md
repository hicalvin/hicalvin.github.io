---
layout: post
title:  "理解iOS内存管理"
date:   2016-10-10 21:07:50 +0800
category: Tech
---

这两天看了来自唐巧的《**iOS开发进阶**》， 对一些iOS的关键问题做个笔记， 加深自己的理解。 

```
- (BOOL)application:(UIApplication *)application didFinishLauchingWithOptions:(NSDictionary *)launchOptions
{  
	NSObject *object = [[NSObject alloc] init];
	NSLog(@"Reference Count = %u", [object retainCount]);
	NSObject *another = [object retain];
	NSLog(@"Reference Count = %u", [object retainCount]);
	[another release];
	NSLog(@"Reference Count = %u", [object retainCount]);
	[object release];
	return YES;
}
```

这段输出应该容易想到。 分别是 1， 2， 1.

但是下面的结果就不一定了： 

```
- (BOOL)application:(UIApplication \*)application didFinishLauchingWithOptions:(NSDictionary \*)launchOptions
{  
	NSObject *object = [[NSObject alloc] init];
	NSLog(@"Reference Count = %u", [object retainCount]);
	[object release];
	NSLog(@"Reference Count = %u", [object retainCount]);
	return YES;
}

```
结果却是 1， 1，  而不是1， 0. 

为什么第二个数值是1 而不是0， 因为最后一次执行release时， 系统知道马上就要回收内存了， 就没必要再降retainCount减1了， 以为不管减不减1， 该对象都肯定会被回收， 而对象被回收后， 它的所有的内存区域， 包括ratainCount也都变的没有意义， 不将这个值从1变为0， 可以减少一次内存的操作， 加速对象回收。 

所以效率至上。 

想象Java的内存管理机制是通过类似有向图的方式， 可达跟节点的就是有效对象， 否则就是无效对象， 可以被GC。 

好，继续iOS。  那么通过引用计数应付不了什么情形呢？ 那就是**循环引用(Reference Cycle)**, 类似于数据库的死锁， A引用B， B引用A， 或者更复杂的A B C D形成引用环， 互相等对方释放。 如果是手动引用还好办， 可以release来手动释放， 但是在ARC的情况下， 就需要另外一种方式了， 那就是**弱引用(Weak Reference)**. 弱引用的意思就是， 虽然持有对象， 但是不增加引用计数， 也就意味着计数由其他对象来控制。 应用场景在delegate中比较多， 因为delegate就是 A B相互引用的情形。 






