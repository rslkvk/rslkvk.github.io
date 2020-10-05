---
layout: post
title: Test post
description: Testtestttest
tags: [java, books]
---

Test diagrams

@startuml
Alice -> Bob: Authentication Request
Bob --> Alice: Authentication Response

Alice -> Bob: Another authentication Request
Alice <-- Bob: Another authentication Response
@enduml

---
Test of Code Highlighting: 

```java
public static void main(String args[]) {
  System.out.println("Hello World");
}
```
---
Diagram as PNG from draw.io

![Diagrams](/assets/diagrams/UntitledDiagram.png)

--- 

```typescript

import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';


@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule
    ],
  providers: [{
    provide: HTTP_INTERCEPTORS,
    useClass: TokenInterceptor,
    multi: true
  },
  {
    provide: HTTP_INTERCEPTORS,
    useClass: ErrorInterceptor,
    multi: true
  }],
  bootstrap: [AppComponent]
})
export class AppModule { }
```
> Two things are infinite: the universe and human stupidity; and I'm not sure about the universe.
> ― Albert Einstein