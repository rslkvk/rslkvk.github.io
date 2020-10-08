---
layout: post
title: How to use Spring Bean with @Autowired in a Apache Camel Predicate
description: How to use Spring Bean with @Autowired in a Apache Camel Predicate. It's part 1 of the Apache Camel knowledge series
tags: [java, apache camel, spring]
---

# Using @Autowired in a Predicate - Apache Ignite

If you have to inject a bean via `@Autowired` within a Camel **Predicate** then you probably may get **`CannotLoadBeanClassException`** Exception from Spring on server startup. 

The solution is that you have to make the Predicate as Spring `@Component` and load it within a camel route as Spring Bean li
ke this: 

```java
@Component
public class CustomPredicate implements Predicate {

    //trying to autowire
    @Autowired
    MyBean myBeanWhichShouldAutowired;
    
    @Override 
    public boolean matches(Exchange exchange) {
        //do something with myBean and return boolean. 
        return myBeanWhichShouldAutowired.doSomthing();
    }
}
```

Here is how you can use it: 

```java
public class myRouteBuilder extends RouteBuilder {

    //... some configurations

    @Override
    public void configure() throws Exception {
        // ...
        from(...)
            .choice()
                .when(spring(CustomPredicate.class))
                    //do something
                .end()
            .end()

        // ...
    }    
}
```


The simplest way to use a Predicate is: 

```java
public class CustomPredicate implements Predicate {
    @Override 
    public boolean matches(Exchange exchange) {
        //do something and return boolean. 
    }
}

public class myRouteBuilder extends RouteBuilder { 

    //... some configurations

    @Override
    public void configure() throws Exception {
        // ...
        from(...)
            .choice()
                .when(new CustomPredicate())
                    //do something
                .end()
            .end()
        // ...
    }    
}
```

> P.S. The code above are just some code snippets. You can't compile & run it.