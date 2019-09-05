---
layout: post
title:  "Switch throw NULL exception, why".
date:   2019-09-05 09:59:50 +0800
category: tech
---
```java
public class SwitchString {
    public static void main(String[] argu) {
        method(null);
    }

    public static void method(String param) {
        switch (param) {

        case "sth": System.out.println("it's sth"); 
            break;
        case "null": System.out.println("it's null"); 
            break;
        default: System.out.println("default");
    } }

```



Output

``` java.lang.NullPointerException
java.lang.NullPointerException
```



原因是在用String作为Switch的参数的时候， switch在运行时使用的其实是 String.equals(). 所以如果传入参数是null，自然会抛空指针。 



如果使用枚举做参数也是一样。 switch使用枚举，实际是调用了 enum.ordinal() 方法，所以如果传入null，同样也会导致空指针。  

所以需要在使用swtich的时候，在方法的最开始有个为空判断。 