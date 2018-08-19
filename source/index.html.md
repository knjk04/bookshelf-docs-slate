---
title: Style guide

language_tabs: # must be one of https://git.io/vQNgJ
  - java
  - xml

toc_footers:
  - <a href='https://github.com/knjk04/Bookshelf'>Bookshelf on GitHub</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:


search: true
---

# Table of contents

1. Introduction

2. File organisation

2. Formatting

3. Naming conventions

4. Good practices

5. XML style

6. Annotations

# 1. Introduction

The style guide we follow is modelled around [Google's Java Style Guide](https://google.github.io/styleguide/javaguide.html). 
Please refer to our style guide instead of Google's if you want to contribute to this repository.

If you see a place where the styleguide is violated, please do submit a pull request.

<aside class="success">
If in doubt, get in contact with us by raising an issue.
</aside>

# 2. File organisation

## 2.1 Import statements

### 2.1.1 No wildcard imports

Please do not use wildcard imports on this repository, even if you need to import several times from a particular package.

### 2.1.2 Remove unused imports

Help keep our files tidy by removing unused imports.

If an import is **commented** out, please do not remove it. Instead, we request that you raise an issue to ask if it is needed. Raising an issue could be really helpul. We might just have forgotten about it.

# 3. Formatting

## 3.1 Braces

### 3.1.1 Optional braces

Braces are always used with ```if/else```, ```for```, ```while``` and ```do``` statements, even when the body consists of no statements or one statement.

### 3.1.2 K & R style nonempty blocks

Braces use the Kernighan and Ritchie style for nonempty blocks or block-like constructs.

### 3.1.3 Empty blocks 

> (Empty blocks) Acceptable:

```java
// Acceptable
public defaultConstructor() {}

// Also acceptable
void foo() { 
}

// Not acceptable
try {
  parseBookListData();
} catch (IOException e) {}

```


An empty block or block-like construct can be in K & R style (see section 3.1.2).

Another option is for the brace to be closed after it has been opened with no characters or line breaks in between (```{}```), except when it is part of a multi-block statement -- 
a block that consists of multiple blocks (e.g. if/else or ```try/catch/finally```).

Note that the unacceptable example above is for illustrative purposes only. It also violates the 'Catch Specific Exception' guideline (see section 6.3)

## 3.2 Spaces around operators

> (Spaces around operators) Acceptable:

```java
// Acceptable
this.pageCount += pageCount;

// Not acceptable
this.pageCount+=pageCount;
```

It's just a lot clearer and nicer to read.


## 3.3 Explicit operator precedence

Even where obvious. use parenthesis to make the ordering explicit. It could save someone else who does not know the precedence rules from having to look it up.

> SECTION X, Explicit operator precedence

```java
// Good
meaningfulVariableName = (2 * SECONDS_IN_MILLIS) + OFFSET; 
```


## 3.4 One statement per line

Where every statement is separated by a line break.

## 3.5 Column limit: 100

For readability purposes. Some exceptions include:

- a long URL
- a TODO statement
- package statements
- import statements and anywhere breaking a statement at the 100 character limit is invalid.

# 4. Naming conventions

## 4.1 Non-constant field names

> Section 4.1, Non-constant field names:

```java
// Good
boolean haveClicked = false;

// Bad
boolean mHaveClicked = false;
```


No "Hungarian Notation" (System or Apps Notation).

## 4.2 Prefixes

### 4.2.1 Files

Type of file | Prefix          |
| ---------- | --------------- | 
| Activity   | ```activity_``` |
| Fragment   | ```fragment_``` |
| Menu       | ```menu_```     | 

### 4.2.2 Suffixes

(Switch to the XML tab to see examples) 


| View             | Suffix       |
| ---------------  | ------------ |
| TextView         | ```Txt```    |
| SimpleDraweeView | ```Drawee``` | 
| Button           | ```Btn```    |

- Adapters to be suffixed with ```Adapter```
  
  ```java
  private BookListAdapter bookListAdapter;
  ```

- ```Layout```s to be suffixed with ```Layout```

```xml
android:id="@+id/constraintLayout
```

# Good practices

## 5.1 final where possible

If something can be made final (e.g. constants), it should be made final.

## 5.2 Use maintained/better libraries

If a third-party library is not maintained, please avoid using it.

If something is deprecated (third-party or not), please also avoid using it.

If there is a better library out there, you should use it (e.g. RecyclerView over ListView).

## 5.3 Minimise variable scope

If something can be local, it should be made local. A variable should be declared as close to where it is used as possible. 

<aside class="success">
This can help reduce the likelihood of a bug occuring, as well as improve readability.
</aside>

## 5.4 Exceptions

### 5.4.1 Catch specific exceptions

Instead of just catching ```Exception```, if it is possible to catch (a) particular exception(s), do so.

```java
// Bad
try {
  // do something fishy
} catch (Exception e) { // lazy
  e.printStackTrace();
}

// Good
try {
  // do something fishy
} catch (NullPointerException e) {
  e.printStackTrace();
}
```

### 5.4.2 Don't drop the catch

In a catch block, don't do nothing by leaving the block empty. You should ideally log the exception or print the stack trace.

``` java
// Good
try {
  execFishyCode();
} catch (IOException e) {
  e.printStackTrace();
}

// Bad
try {
  execFishyCode();
} catch (IOException e) {
}
```

## 5.5 String arrays use string resources

(Switch to XML tab to see example)

Instead of using string literals, string arrays should always use String resources. Array string literals are not translated, whereas String resources are.

```xml
<!-- Good -->
<string-array name="bookInfoShortened">
  <item> @string/title </item>
  <item> @string/publishedDate </item>
  <item> @string/publisher </item>
</string-array>

<!-- Bad -->
<string-array name="bookInfoShortened">
  <item>title</item>
  <item>publishedDate</item>
  <item>publisher</item>
</string-array>
```

## 5.6 Use single positive conditionals

It can be a lot confusing for other programmers (see [Fowler's article](https://www.refactoring.com/catalog/removeDoubleNegative.html)).

```java
// Good
if (isAvailable) {
  // do something
}

// Bad
if (!isNotAvailable()) {
  // do something
}
```

## 5.7 Class member ordering

This section has been modified from the [Ribot Android style guide](https://github.com/ribot/android-guidelines/blob/master/project_and_code_guidelines.md). 
It is licensed under the Apache license.

As the Ribot style guide points out, there is no one correct way of ordering members. However, following this format can help find, for example, private methods easier.

The following order should be used:

1. Constants
2. Fields
3. Constructors
4. Overidden methods and callbacks (public or private)
5. Public methods
6. Private methods
7. Inner classes or interfaces

> Class member ordering

```java
public class MainActivity extends Activity {

    private static final String TAG = MainActivity.class.getSimpleName();

    private String title;
    private TextView textViewTitle;

    @Override
    public void onCreate() {
        ...
    }

    public void setTitle(String title) {
    	this.title = title;
    }

    private void setUpView() {
        ...
    }

    static class InnerClass {

    }
}
```

Activity or Fragment classes should follow the ordering or the activity/fragment lifecycle: ```onCreate()```, ```onDestroy```, ```onPause()``` and ```onResume()```.

> Activity lifecycle

```java
public class MainActivity extends Activity {

	// Order of methods corresponds to the order of the activity lifecycle
    @Override
    public void onCreate() {}

    @Override
    public void onResume() {}

    @Override
    public void onPause() {}

    @Override
    public void onDestroy() {}

}
```

# 6 XML Style

## 6.1 Self-closing

Use self-closing tags where possible.

# 7 Annotations

## 7.1 Annotations on separate lines

Every annotation should be on its own separate line

```java
@NonNull
@Override
private void foo() { ... }
```

## 7.2 Overriding methods

Where a method is overriden from a superclass, the ```@Override``` annotation should be used.
