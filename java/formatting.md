# Formatting for Java

* [Oracle's Naming Conventions](https://www.oracle.com/java/technologies/javase/codeconventions-namingconventions.html)

## Aims
Although Oracle's standards[^1] are much more beginner friendly, it becomes much more difficult for a Java Power user to navigate and write code efficiently. The sheer verbosity of some of the mechanics within Java makes it very tedious to constantly expand certain things out. For example, single expression methods become very tedious to constantly expand out:

```java
// Oracle Conventions
public void helloWorld() {
  System.out.println("Hello World!");
}

// Improved Conventions
public void hello_world()
{ System.out.println("Hello World"); }
```

One lining the entire expression makes sure the 

## Comparison
A quick comparison

<strong>Oracle Standards</strong>

```java
package com.jackmeng.examples;

import static java.lang.System.*;

public class Point implements Serializable {
  private int x;
  private int y;

  public Point(int x, int y) {
    this.x = x;
    this.y = y;
  }

  public int getX() {
    return x;
  }

  public int getY() {
    return y;
  }

  @Override
  public String toString() {
    return "(" + x + ", " + y + ")";
  }

  public static void main(String[] args) throws Exception {
    Point pt = new Point(3, 4);
    out.println(pt);
  }
}
```

<strong>Improved Conventions</strong>

```java
package com.jackmeng.examples;

import static java.lang.System.*;

public class Point
  	implements
  	Serializable
{
  private int x, y;

  public Point(int x, int y)
  { this.x = x; this.y = y; }

  public int getX() { return x; }

  public int getY() { return y; }

  @Override public String toString()
  { return "(" + x + ", " + y + ")"; }

  public static void main(String[] args)
		throws Exception
  {
    out.println(
      new Point(3, 4)
    );
  }
}
```

## Naming Conventions
Although it is widely acknowledged that programmer definable structures (e.g. variables, types, etc..) should be left up to the programmer, they should often follow a guideline to avoid ambiguity and verbosity.

### Footnotes
[^1]: *“Code Conventions for the Java Programming Language.”* Code Conventions for the Java Programming Language: 1. Introduction, 20 Apr. 1999, www.oracle.com/java/technologies/javase/codeconventions-introduction.html.
