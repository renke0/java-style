# Java Style Guide

## Table of contents

* [Introduction](#introduction)
  * [Resources](#resources)
* [Source file basics](#source-file-basics)
  * [File name](#file-name)
  * [File encoding](#file-encoding)
  * [Whitespace characters](#whitespace-characters)
  * [Special escape sequences](#special-escape-sequences)
  * [Non-ASCII characters](#non-ascii-characters)
* [Source file structure](#source-file-structure)
  * [License or copyright information](#license-or-copyright-information)
  * [Package statement](#package-statement)
  * [Import statements](#import-statements)
    * [No wildcard imports](#no-wildcard-imports)
    * [No line wrapping](#no-line-wrapping)
    * [Ordering and spacing](#ordering-and-spacing)
    * [Static imports](#static-imports)
  * [Class declaration](#class-declaration)
    * [Top-level class declaration](#top-level-class-declaration)
    * [Ordering of class contents](#ordering-of-class-contents)
* [Formatting](#formatting)
  * [Braces](#braces)
    * [Block statements](#block-statements)
    * [Non-empty blocks](#non-empty-blocks)
    * [Empty blocks](#empty-blocks)
  * [Tabs and indentation](#tabs-and-indentation)
    * [Block indentation](#block-indentation)
    * [Where to break](#where-to-break)
    * [Wrapped lines indentation](#wrapped-lines-indentation)
    * [Method and constructor declaration indentation](#method-and-constructor-declaration-indentation)
    * [Method and constructor call indentation](#method-and-constructor-call-indentation)
  * [Character limit](#character-limit)
  * [Whitespace](#whitespace)
    * [Vertical whitespace](#vertical-whitespace)
    * [Horizontal whitespace](#horizontal-whitespace)
    * [Horizontal alignment](#horizontal-alignment)
  * [Grouping parentheses](#grouping-parentheses)
  * [Specific constructs](#specific-constructs)
    * [Enum classes](#enum-classes)
    * [Variable declarations](#variable-declarations)
    * [Arrays](#arrays)
    * [Switch statements](#switch-statements)
    * [Annotations](#annotations)
    * [Comments](#comments)
    * [Constants](#constants)
    * [Modifiers](#modifiers)
    * [Numeric Literals](#numeric-literals)
    * [Class fields](#class-fields)
    * [Constructors](#constructors)
    * [Methods](#methods)
    * [Inner classes](#inner-classes)
* [Naming](#naming)
  * [Naming rules common to all identifiers](#naming-rules-common-to-all-identifiers)
  * [Naming rules by identifier type](#naming-rules-by-identifier-type)
    * [Package names](#package-names)
    * [Class names](#class-names)
    * [Method names](#method-names)
    * [Constant names](#constant-names)
    * [Non-constant field names](#non-constant-field-names)
    * [Parameter names](#parameter-names)
    * [Local variable names](#local-variable-names)
    * [Type variable names](#type-variable-names)
  * [Camelcase defined](#camelcase-defined)
* [Programming Practices](#programming-practices)
  * [Using `@Override`](#using-override)
  * [Exception handling](#exception-handling)
  * [Static members](#static-members)
  * [Finalizers](#finalizers)
* [Javadoc](#javadoc)
  * [Formatting](#formatting-1)
    * [General form](#general-form)
    * [Paragraphs](#paragraphs)
    * [Block tags](#block-tags)
  * [The summary fragment](#the-summary-fragment)
  * [Where Javadoc is used](#where-javadoc-is-used)
    * [Non-required Javadoc](#non-required-javadoc)

## Introduction

This guide was based on the [Google Java Style Guide][1], but contains several changes and
additions to improve code readability and maintainability. It also adds more examples of *"dos"*
and *"don'ts"*.

### Resources

  The project contains the following resources to aid on the use of this styleguide:

  * An IntelliJIDEA style file, for formatting the code according to the rules described on this
  guide

    > `intellij-style.xml`

  * A [Checkstyle][5] configuration file covering most of the formatting cases described on this
  guide is available in the project

    > `checkstyle.xml`

## Source file basics

### File name

The source file name consists of the case-sensitive name of the top-level class it contains (of
which there is exactly one), plus the `.java` extension.

[⇧Back to the top](#java-style-guide)

### File encoding

Source files are encoded in **UTF-8**.

[⇧Back to the top](#java-style-guide)

### Whitespace characters

Aside from the line terminator sequence, the **ASCII horizontal space character (0x20)** is the
only whitespace character that appears anywhere in a source file. This implies that:

  1. All other whitespace characters in string and character literals are escaped.
  2. Tab characters are **not** used for indentation.

[⇧Back to the top](#java-style-guide)

### Special escape sequences

For any character that has a [special escape sequence][2] (`\b`, `\t`, `\n`, `\f`, `\r`, `\"`, `\'`
and `\\`), that sequence is used rather than the corresponding octal (e.g. `\012`) or Unicode (e.g.
`\u000a`) escape.

[⇧Back to the top](#java-style-guide)

### Non-ASCII characters
For the remaining non-ASCII characters, either the actual Unicode character (e.g. ∞) or the
equivalent Unicode escape (e.g. \u221e) is used. The choice depends only on **which makes the code
easier to read and understand**, although Unicode escapes outside string literals and comments are
strongly discouraged.

| Example                                                | Discussion                                                              |
|--------------------------------------------------------|-------------------------------------------------------------------------|
|`String unitAbbrev = "μs";`                             |Best: perfectly clear even without a comment.                            |
|`String unitAbbrev = "\u03bcs"; // "μs"`                |Allowed, but there's no reason to do this.                               |
|`String unitAbbrev = "\u03bcs"; // Greek letter mu, "s"`|Allowed, but awkward and prone to mistakes.                              |
|`String unitAbbrev = "\u03bcs";`                        |Poor: the reader has no idea what this is.                               |
|`return '\ufeff' + content; // byte order mark`         |Good: use escapes for non-printable characters, and comment if necessary.|

>**Tip:** Never make your code less readable simply out of fear that some programs might not
handle non-ASCII characters properly. If that should happen, those programs are **broken** and they
must be **fixed**.

[⇧Back to the top](#java-style-guide)

## Source file structure

A source file consists of, **in order**:

  1. License or copyright information, if present
  2. Package statement
  3. Import statements
  4. Exactly one top-level class

**Exactly one blank line** separates each section that is present.

[⇧Back to the top](#java-style-guide)

### License or copyright information

If the file has some license or copyright information, the pace to add it is at the beginning of
the file

[⇧Back to the top](#java-style-guide)

### Package statement

The package statement is **not line-wrapped**. [The character limit](#character-limit) does not
apply to package statements.

[⇧Back to the top](#java-style-guide)

### Import statements

#### No wildcard imports

**Wildcard imports**, static or otherwise, **are not used**, due to leading to mistakes and being
error prone.

[⇧Back to the top](#java-style-guide)

#### No line wrapping

Import statements are **not line-wrapped**. [The character limit](#character-limit) does not apply
to import statements.

[⇧Back to the top](#java-style-guide)

#### Ordering and spacing

Imports are ordered as follows:

  1. All static imports in a single block.
  2. All non-static imports in a single block.

If there are both static and non-static imports, a single blank line separates the two blocks.
There are no other blank lines between import statements.

Within each block the imported names appear in ASCII sort order.

[⇧Back to the top](#java-style-guide)

#### Static imports

Static import is not used for static nested classes. They are imported with normal imports.

[⇧Back to the top](#java-style-guide)

### Class declaration

#### Top-level class declaration

Each top-level class resides in a source file of its own.

[⇧Back to the top](#java-style-guide)

#### Ordering of class contents

A class body consists of, **in order**:

  1. Constants
  2. Class fields
  3. Constructors
  4. Methods
  5. Inner classes

**Exactly one blank line** separates each section that is present.

> **Note:** All elements of the class body are optional

[⇧Back to the top](#java-style-guide)

## Formatting

### Braces

#### Block statements

Block structures always **require** braces, even when optional (one liners `if`, `else`, `for`,
`do` and `while`)

```java
// good
if (bacon > life) {
  return bacon;
} else {
  return life;
}
```

```java
// good
for (String magicalItem : magicalItemList) {
  doMagicWith(magicalItem);
}
```

```java
// bad
if (bacon > life)
  return bacon;
else
  return life;
```

```java
// bad
for (String magicalItem : magicalItemList) 
  doMagicWith(magicalItem);
```

[⇧Back to the top](#java-style-guide)

#### Non-empty blocks

Braces positioning for non-empty blocks should follow the [Egyptian Brackets style][3]:

  * No line break before the opening brace.
  * Line break after the opening brace.
  * Line break before the closing brace.
  * Line break after the closing brace, *only if* that brace terminates a statement or terminates
  the body of a method, constructor, or named class. For example, there is *no* line break after
  the brace if it is followed by `else` or a comma.

```java
// good
class SpectacularNameHere {
  public void doStuff() {
    if (stuffIsAlreadyHappening()) {
      waitForStuffToBeDone();
    } else {
      try {
        startNewStuff();
      } catch (StuffException e) {
          recover(e);
      }
    }
  }
}
```

```java
// bad
class ThisIsntDotNet
{
  void whyDoYouDoThis()
  {
    quit();
  }
}
```

A few exceptions for enum classes are given in section [Enum classes](#enum-classes).

[⇧Back to the top](#java-style-guide)

#### Empty blocks

Braces positioning on empty blocks should be concise, by positioning the closing bracket right 
after the opening one. This rule should be applied unless the block is part of a *multiblock 
statement* (ie. `try/catch/finally`, `if/else`).

```java
// good
public void unimplemented() {}
```

```java
// good
class EmptyClass {}
```

```java
// good
public void exceptionIgnorer() {
  try {
    doSomething();
  } catch (Exception e) {
  }
}
```

```java
// bad
public void unimplemented() {
}
```

```java
// bad
class EmptyClass {
}
```

```java
// bad
public void exceptionIgnorer() {
  try {
    doSomething();
  } catch (Exception e) {}
}
```

 
[⇧Back to the top](#java-style-guide)

### Tabs and indentation

#### Block indentation

The class blocks should be indented with two space characters (0x20). The tab character should not
be used in any part of the document.

```java
// good
class Spaceship {
  String licensePlate;
  int maximumSpeed;

  void setMaximumSpeed(int maximumSpeed) {
    this.maximumSpeed = maximumSpeed;
  }
}
```

```java
// bad - using 4 spaces
class Spaceship {
    String licensePlate;
    int maximumSpeed;

    void setMaximumSpeed(int maximumSpeed) {
      this.maximumSpeed = maximumSpeed;
    }
}
```

```java
// bad - using tabs
class Spaceship {
	String licensePlate;
	int maximumSpeed;

	void setMaximumSpeed(int maximumSpeed) {
		this.maximumSpeed = maximumSpeed;
	}
}
```

[⇧Back to the top](#java-style-guide)

#### Where to break

  The prime directive of line-wrapping is: **prefer to break at a higher syntactic level**. Also:

  1. When a line is broken at a *non-assignment* operator the break comes before the symbol.
      * This also applies to the following "operator-like" symbols:
        * the dot separator (`.`)
        * the two colons of a method reference (`::`)
        * an ampersand in a type bound (`<T extends Foo & Bar>`)
        * a pipe in a catch block (`catch (FooException | BarException e)`).
  2. When a line is broken at an *assignment* operator the break typically comes *after* the
  symbol.
      * This also applies to the "assignment-operator-like" colon in an enhanced *for* ("foreach")
      statement.
  3. A method or constructor name stays attached to the open parenthesis (`(`) that follows it.
  4. A comma (`,`) stays attached to the token that precedes it.
  5. A line is never broken adjacent to the arrow (`->`) in a lambda, except that a break may come
  immediately after the arrow if the body of the lambda consists of a single unbraced expression.

> **Note:** Note: The primary goal for line wrapping is to have clear code, *not necessarily* code
that fits in the smallest number of lines.

[⇧Back to the top](#java-style-guide)

#### Wrapped lines indentation

Lines exceeding the [limit of 100 characters](#character-limit) per line should be continued with a
doubled indentation (4 spaces + the current indentation for the line)

```java
// good
void getValue() {
  exceptionallyLongVariableName
      .getCuriouslyExtensivePropertyName();
}
```

```java
// bad
void getValue() {
  exceptionallyLongVariableName
    .getCuriouslyExtensivePropertyName();
}
```

[⇧Back to the top](#java-style-guide)

#### Method and constructor declaration indentation

Method and constructor declaration parameters can be wrapped to not exceed the
[100 character limit](#character-limit) or to improve the readability of the code.

When wrapping the metod/constructor parameters the following rules apply:

  1. The first parameter should be placed in the following line to the method or constructor name,
  [but with doubled indentation](#wrapped-lines-indentation) (+4 spaces)
  2. All the subsequent lines should be aligned with the first parameter.
  3. The closing parenthesis of the parameter list and semicolon should be in the same line as the
  last parameter is.
  5. Every parameter should be in a new line.

```java
// good - avoid the parameter and its modifiers/annotations to be split
public static void exceptionallyLongMethodName(
    @NonNull @Validated("minValue") final Integer minimumValue,
    Integer maximumValue,
    String message) {
```

```java
// bad
public static void exceptionallyLongMethodName(Integer minimumValue,
    Integer maximumValue, String message) {
```

```java
// bad
public static void exceptionallyLongMethodName(Integer minimumValue, Integer
    maximumValue) {
```

```java
// bad
public static void exceptionallyLongMethodName(
    @NonNull
    @Validated("minValue")
    final Integer minimumValue,
    Integer maximumValue,
    String message) {
```

[⇧Back to the top](#java-style-guide)

#### Method and constructor call indentation

Method and constructor call parameters can be wrapped to not exceed the 
[100 character limit](#character-limit) or to improve the readability of the code.

When wrapping the method/constructor parameters the following rules apply:

  1. The first parameter should be placed in the following line to the method/constructor name,
  [but with doubled indentation](#wrapped-lines-indentation) (+4 spaces).
  2. All the subsequent lines should be aligned with the first parameter.
  3. The closing parenthesis of the parameter list and opening curly brace of the method body
  should be in the same line as the last parameter is.
  4. *Optionally*, every new parameter can be placed on a new line.

```java
// good
String exceptionallyLongVariableName = exceptionallyLongMethodName(
    minimumValue, 3, "name") {
```

```java
// good
String exceptionallyLongVariableName = exceptionallyLongMethodName(
    minimumValue, 
    3, 
    "name") {
```

```java
// bad
String exceptionallyLongVariableName = exceptionallyLongMethodName(minimumValue, 
    3, "name") {
```

[⇧Back to the top](#java-style-guide)

### Character limit

The lines should not exceed *100 columns*, with the following exceptions:

  * Lines where it is impossible to keep the 100 columns limit, like a long URL on a javadoc
  comment, or a reference to a method with an excessively long name.
  * `package` and `import` statements (see [Package statement](#package-statement) and
  [Import statements](#import-statements))

[⇧Back to the top](#java-style-guide)

### Whitespace

#### Vertical whitespace

A single blank line appears:

  1. *Between* consecutive members or initializers of a class: fields, constructors, methods,
  nested classes, static initializers, and instance initializers.
      * **Exception:** A blank line between two consecutive fields (having no other code between
      them) is optional. Such blank lines are used as needed to create *logical groupings* of
      fields.
      * **Exception:** Blank lines between enum constants are covered in section
      [Enum classes](#enum-classes).
  2. Between statements, *as needed* to organize the code into logical subsections.
  3. As required by other sections of this document (such as
  [Source file structure](#source-file-structure) and [Import statements](#import-statements).
  4. At the end of the file, as otherwise this generates a false positive on changed lines for
  VCS systems.

Multiple consecutive blank lines are **not** permitted.

[⇧Back to the top](#java-style-guide)

#### Horizontal whitespace

Beyond where required by the language or other style rules, and apart from literals, comments and
Javadoc, a single ASCII space also appears in the following places **only**.

  1. Separating any reserved word, such as `if`, `else`, `for` or `catch`, from an open parenthesis
  (`(`) that follows it on that line.
  2. Separating any reserved word, such as `else` or `catch`, from a closing curly brace (`}`) that
  precedes it on that line.
  3. Before any open curly brace (`{`), including array initializers: `new int[] { 5, 6 }`
  4. On both sides of any binary or ternary operator. This also applies to the following
  "operator-like" symbols:
      * the ampersand in a conjunctive type bound: `<T extends Foo & Bar>`
      * the pipe for a catch block that handles multiple exceptions:
      `catch (FooException | BarException e)`
      * the colon (`:`) in an enhanced `for` ("foreach") statement : `for (int i : intArray) {`
      * the arrow in a lambda expression: `(String str) -> str.length()`
        * **Exception:** the two colons (`::`) of a method reference, which is written like
        `Object::toString`
        * **Exception:** the dot separator (`.`), which is written like `object.toString()`
  5. After `,:;` or the closing parenthesis (`)`) of a cast.
  6. On both sides of the double slash (`//`) that begins an end-of-line comment. Here, multiple
  spaces are allowed, but not required.
  7. Between the type and variable of a declaration: `List<String> list`

This rule is never interpreted as requiring or forbidding additional space at the start or end of a
line; it addresses only *interior* space.

[⇧Back to the top](#java-style-guide)

#### Horizontal alignment

> **Terminology Note:** Horizontal alignment is the practice of adding a variable number of
additional spaces in your code with the goal of making certain tokens appear directly below certain
other tokens on previous lines.

This practice is strongly discouraged, and is never required. It is not even required to maintain
horizontal alignment in places where it was already used.

```java
// good
private int x;
private Color color;
```

```java
// discouraged
private int   x;
private Color color;
```

> **Tip:** Alignment can aid readability, but it creates problems for future maintenance. Consider
a future change that needs to touch just one line. This change may leave the formerly-pleasing
formatting mangled, and that is **allowed**. More often it prompts the coder (perhaps you) to
adjust whitespace on nearby lines as well, possibly triggering a cascading series of reformattings.
That one-line change now has a "blast radius." This can at worst result in pointless busywork, but
at best it still corrupts version history information, slows down reviewers and exacerbates merge
conflicts.

[⇧Back to the top](#java-style-guide)

### Grouping parentheses

Optional grouping parentheses are omitted only when author and reviewer agree that there is no
reasonable chance the code will be misinterpreted without them, nor would they have made the code
easier to read. It is not reasonable to assume that every reader has the entire Java operator
precedence table memorized.

[⇧Back to the top](#java-style-guide)

### Specific constructs

#### Enum classes

After each comma that follows an enum constant, a line break is optional. Additional blank lines
are also allowed only when the constant has methods. An enum class with no methods and no
documentation on its constants may optionally be formatted as if it were an array initializer:
`private enum Suit { CLUBS, HEARTS, SPADES, DIAMONDS }`

```java
// good
private enum Answer {
  YES {
    @Override public String toString() {
      return "yes";
    }
  },
  NO,
  MAYBE
}
```

```java
// good
private enum Answer {
  YES, NO, MAYBE
}
```

```java
// good
private enum Answer {
  YES,
  NO,
  MAYBE
}
```

```java
// good
private enum Answer { YES, NO, MAYBE }
```

```java
// bad
private enum Answer {
  YES {
    @Override public String toString() {
      return "yes";
    }
  }, NO, MAYBE
}
```

> **Tip:** When choosing between breaking lines or keeping them on a single line, choose only one
strategy per enum class. If there are enums enough to exceed the
[maximum line length](#character-limit), consider breaking using the "one line per constant"
strategy

[⇧Back to the top](#java-style-guide)

#### Variable declarations

Every variable declaration (field or local) declares only one variable: declarations such as
`int a, b;` are not used.

  * **Exception:** Multiple variable declarations are acceptable in the header of a `for` loop.

Local variables are not habitually declared at the start of their containing block or block-like
construct. Instead, local variables are declared close to the point they are first used (within
reason), to minimize their scope. Local variable declarations typically have initializers, or are
initialized immediately after declaration.

[⇧Back to the top](#java-style-guide)

#### Arrays

Arrays are initialized as "block-like constructs". All of the following are acceptable:

```java
// good
new int[] { 0, 1, 2, 3 }
```

```java
// good
new int[] {
  0, 1, 2, 3
}
```

```java
// good
new int[] {
  0,
  1,
  2,
  3,
}
```

> The rules specified on section [Horizontal whitespace](#horizontal-whitespace) must be observed

The square brackets form a part of the *type*, not the variable.

```java
// good
String[] args
```

```java
// bad
String args[]
```

[⇧Back to the top](#java-style-guide)

#### Switch statements

> **Terminology Note:** Inside the braces of a *switch block* are one or more *statement groups*.
Each statement group consists of one or more *switch labels* (either `case FOO:` or `default:`),
followed by one or more statements (or, for the *last* statement group, *zero* or more statements).

As with any other block, the contents of a switch block are indented +2. After a switch label,
there is a line break, and the indentation level is increased +2, exactly as if a block were being
opened. The following switch label returns to the previous indentation level, as if a block had
been closed.

```java
// good
switch (input) {
  case 1:
    return processFirst();
  case 2:
    return processTwo();
  case 3:
    return processThree()
  default:
    break;
}
```

```java
// bad
switch (input) {
case 1:
  return processFirst();
case 2:
  return processTwo();
case 3:
  return processThree()
default:
  break;
}
```

Within a switch block, each statement group either terminates abruptly (with a `break`, `continue`,
`return` or thrown exception), or is marked with a comment to indicate that execution will or
*might* continue into the next statement group. Any comment that communicates the idea of
fall-through is sufficient (typically `// fall through`). This special comment is not required in
the last statement group of the switch block.

```java
// good
switch (input) {
  case 1:
  case 2:
    prepareOneOrTwo();
    // fall through
  case 3:
    handleOneTwoOrThree();
    break;
  default:
    handleLargeNumber(input);
}
```

> Notice that no comment is needed after `case 1:`, only at the end of the statement group.

Each switch statement includes a `default` statement group, even if it contains no code.

  * **Exception:** A switch statement for an `enum` type may omit the default statement group, *if*
  it includes explicit cases covering *all* possible values of that type. This enables IDEs or
  other static analysis tools to issue a warning if any cases were missed.

[⇧Back to the top](#java-style-guide)

#### Annotations

Annotations applying to a class, method or constructor appear immediately after the documentation
block, and each annotation is listed on a line of its own (that is, one annotation per line). These
line breaks do not constitute line-wrapping, so the indentation level is not increased. Example:

```java
@Override
@Nullable
public String getNameIfPresent() { ... }
```

  * **Exception:** A single parameterless annotation *may* instead appear together with the first
  line of the signature, for example:

```java
@Override public int hashCode() { ... }
```

Annotations applying to a field also appear immediately after the documentation block, but in this
case, *multiple* parameterless annotations may be listed on the same line; for example:

```java
@Partial @Mock DataLoader loader;
```

Annotations applying to any scope and specifying only the `value` element should omit the element
key.

```java
// good
@Inject("inputField")
String input;
```

```java
// good
@Inject(value = "inputField")
String input;
```

Annotations applying to any scope and not specifying any elements should not have parentheses.

```java
// good
@Entity
class Person { ... }
```

```java
// bad
@Entity()
class Person { ... }
```

[⇧Back to the top](#java-style-guide)

#### Comments

This section addresses implementation comments. Javadoc is addressed separately in section
[Javadoc](#javadoc).

Any line break may be preceded by arbitrary whitespace followed by an implementation comment. Such
a comment renders the line non-blank.

Block comments are indented at the same level as the surrounding code. They may be in `/* ... */`
style or `// ...` style. For multi-line `/* ... */` comments, subsequent lines must start with `*`
aligned with the * on the previous line.

Inline comments (`// ...`) should not span multiple lines when added to the end of a line already
containing code.

The `/** ... */` code style is reserved for Javadoc blocks only.

Comments are not enclosed in boxes drawn with asterisks or other characters.

```java
/*
 * This is
 * okay.
 */
 ```

```java
 // This is
 // okay.
```

```java
/* This is
 * okay. */
```

```java
String input; // This is
              // not okay
```

```java
/********************
 * This is not okay *
 ********************/
```

> **Tip:** When writing multi-line comments, use the `/* ... */` style if you want automatic code
formatters to re-wrap the lines when necessary (paragraph-style). Most formatters don't re-wrap
lines in `// ...` style comment blocks.

#### Constants

[⇧Back to the top](#java-style-guide)

#### Modifiers

Class and member modifiers, when present, appear in the order recommended by the *Java Language
Specification*:

    public protected private abstract default static final transient volatile synchronized native strictfp

[⇧Back to the top](#java-style-guide)

#### Numeric Literals

`long` valued integer literals use an uppercase `L` suffix, never lowercase (to avoid confusion
with the digit `1`). For example, `3000000000L` rather than `3000000000l`.

[⇧Back to the top](#java-style-guide)

#### Class fields

[⇧Back to the top](#java-style-guide)

#### Constructors

[⇧Back to the top](#java-style-guide)

#### Methods

[⇧Back to the top](#java-style-guide)

#### Inner classes

[⇧Back to the top](#java-style-guide)

## Naming

### Naming rules common to all identifiers

Identifiers use only ASCII letters and digits, and, in a small number of cases noted below,
underscores. Thus each valid identifier name is matched by the regular expression `\w+` .

Special prefixes or suffixes, like those seen in the examples `name_`, `mName`, `s_name` and
`kName`, are not used.

[⇧Back to the top](#java-style-guide)

### Naming rules by identifier type

#### Package names

Package names are all lowercase, with consecutive words simply concatenated together (no
underscores). For example, `com.example.deepspace`, not `com.example.deepSpace` or
`com.example.deep_space`.

[⇧Back to the top](#java-style-guide)

#### Class names

Class names are written in [UpperCamelCase](#camelcase-defined).

Class names are typically nouns or noun phrases. For example, `Character` or `ImmutableList`.
Interface names may also be nouns or noun phrases (for example, `List`), but may sometimes be
adjectives or adjective phrases instead (for example, `Readable`).

There are no specific rules or even well-established conventions for naming annotation types.

Test classes are named starting with the name of the class they are testing, and ending with
`Test`. For example, `HashTest` or `HashIntegrationTest`.

[⇧Back to the top](#java-style-guide)

#### Method names

Method names are written in [lowerCamelCase](#camelcase-defined).

Method names are typically verbs or verb phrases. For example, `sendMessage` or `stop`.

Underscores may appear in JUnit test method names to separate logical components of the name, with
each component written in [lowerCamelCase](#camelcase-defined). The used pattern is
`<methodUnderTest>_<state>`, for example `pop_emptyStack` or `findUser_throwException`.

[⇧Back to the top](#java-style-guide)

#### Constant names

Constant names use `CONSTANT_CASE` or `SCREAMING_SNAKE_CASE`: all uppercase letters, with each word
separated from the next by a single underscore. But what is a constant, exactly?

Constants are static final fields whose contents are deeply immutable and whose methods have no
detectable side effects. This includes primitives, Strings, immutable types, and immutable
collections of immutable types. If any of the instance's observable state can change, it is not a
constant. Merely *intending* to never mutate the object is not enough. Examples:

```java
// Constants
static final int NUMBER = 5;
static final ImmutableList<String> NAMES = ImmutableList.of("Ed", "Ann");
static final ImmutableMap<String, Integer> AGES = ImmutableMap.of("Ed", 35, "Ann", 32);
static final Joiner COMMA_JOINER = Joiner.on(','); // because Joiner is immutable
static final SomeMutableType[] EMPTY_ARRAY = {};
enum SomeEnum { ENUM_CONSTANT }

// Not constants
static String nonFinal = "non-final";
final String nonStatic = "non-static";
static final Set<String> mutableCollection = new HashSet<String>();
static final ImmutableSet<SomeMutableType> mutableElements = ImmutableSet.of(mutable);
static final ImmutableMap<String, SomeMutableType> mutableValues =
   ImmutableMap.of("Ed", mutableInstance, "Ann", mutableInstance2);
static final Logger logger = Logger.getLogger(MyClass.getName());
static final String[] nonEmptyArray = {"these", "can", "change"};
```

These names are typically nouns or noun phrases.

[⇧Back to the top](#java-style-guide)

#### Non-constant field names

Non-constant field names (static or otherwise) are written in [lowerCamelCase](#camelcase-defined).

These names are typically nouns or noun phrases. For example, `computedValues` or `index`.

[⇧Back to the top](#java-style-guide)
#### Parameter names

Parameter names are written in [lowerCamelCase](#camelcase-defined).

One-character parameter names should be avoided.

[⇧Back to the top](#java-style-guide)

#### Local variable names

Local variable names are written in [lowerCamelCase](#camelcase-defined).

Even when final and immutable, local variables are not considered to be constants, and should not
be styled as constants.

[⇧Back to the top](#java-style-guide)

#### Type variable names

Each type variable is named in one of two styles:

  * A single capital letter, optionally followed by a single numeral (such as `E`, `T`, `X`, `T2`)
  * In case of a bounded parameter, optionally the name in the form used for classes (see
  [Class names](#class-names) followed by the capital letter `T` can be used (examples:
  `<RequestT extends Request>`, `<FooBarT extends FooBar>`).

[⇧Back to the top](#java-style-guide)

### Camelcase defined

Sometimes there is more than one reasonable way to convert an English phrase into camelcase, such
as when acronyms or unusual constructs like "IPv6" or "iOS" are present. To improve predictability,
this style guide specifies the following (nearly) deterministic scheme.

Beginning with the prose form of the name:

  1. Convert the phrase to plain ASCII and remove any apostrophes. For example, "Müller's
  algorithm" might become "Mullers algorithm".
  2. Divide this result into words, splitting on spaces and any remaining punctuation (typically
  hyphens).
      * *Recommended:* if any word already has a conventional camelcase appearance in common
      usage, split this into its constituent parts (e.g., "AdWords" becomes "ad words"). Note that
      a word such as "iOS" is not really in camelcase *per se*; it defies *any* convention, so
      this recommendation does not apply.
  3. Now lowercase everything (including acronyms), then uppercase only the first character of:
      * ... each word, to yield *upper camelcase*, or
      * ... each word except the first, to yield *lower camelcase*
  4. Finally, join all the words into a single identifier.

Note that the casing of the original words is almost entirely disregarded. Examples:

| Prose form              | Correct             | Incorrect           |
|-------------------------|---------------------|---------------------|
| "XML HTTP request"      | `XmlHttpRequest`    | `XMLHTTPRequest`    |
| "new customer ID"       | `newCustomerId`     | `newCustomerID`     |
| "inner stopwatch"       | `innerStopwatch`    | `innerStopWatch`    |
| "supports IPv6 on iOS?" | `supportsIpv6OnIos` | `supportsIPv6OnIOS` |
| "YouTube importer"      | `YouTubeImporter`   | `YoutubeImporter`   |

> **Note:** Some words are ambiguously hyphenated in the English language: for example "nonempty"
and "non-empty" are both correct, so the method names `checkNonempty` and `checkNonEmpty` are
likewise both correct.

[⇧Back to the top](#java-style-guide)

## Programming Practices

### Using `@Override`

A method is marked with the `@Override` annotation whenever it is legal. This includes a class
method overriding a superclass method, a class method implementing an interface method, and an
interface method respecifying a superinterface method.

  * **Exception:** `@Override` may be omitted when the parent method is `@Deprecated`.

[⇧Back to the top](#java-style-guide)

### Exception handling

Except as noted below, it is very rarely correct to do nothing in response to a caught exception.
(Typical responses are to log it, or if it is considered "impossible", rethrow it as an
`AssertionError`.)

When it truly is appropriate to take no action whatsoever in a catch block, the reason this is
justified is explained in a comment.

```java
try {
  int i = Integer.parseInt(response);
  return handleNumericResponse(i);
} catch (NumberFormatException ok) {
  // it's not numeric; that's fine, just continue
}
return handleTextResponse(response);
```

  * **Exception:** In tests, a caught exception may be ignored without comment *if* its name is or
  begins with `expected`. The following is a very common idiom for ensuring that the code under
  test does throw an exception of the expected type, so a comment is unnecessary here.

```
try {
  emptyStack.pop();
  fail();
} catch (NoSuchElementException expected) {
}
```

[⇧Back to the top](#java-style-guide)

### Static members

When a reference to a static class member must be qualified, it is qualified with that class's
name, not with a reference or expression of that class's type.

```java
Foo aFoo = ...;
Foo.aStaticMethod(); // good
aFoo.aStaticMethod(); // bad
somethingThatYieldsAFoo().aStaticMethod(); // very bad
```

[⇧Back to the top](#java-style-guide)

### Finalizers

It is extremely rare to override `Object.finalize`.

> **Tip:** Don't do it. If you absolutely must, first read and understand
[Effective Java Item 7][4], "Avoid Finalizers," very carefully, and **then don't do it**.

[⇧Back to the top](#java-style-guide)

## Javadoc

### Formatting

#### General form

The *basic* formatting of Javadoc blocks is as seen in this example:

```java
/**
 * Multiple lines of Javadoc text are written here,
 * wrapped normally...
 */
public int method(String p1) { ... }
```

... or in this single-line example:

```java
/** An especially short bit of Javadoc. */
```

The basic form is always acceptable. The single-line form may be substituted when the entirety of
the Javadoc block (including comment markers) can fit on a single line. Note that this only applies
when there are no block tags such as `@return`.

[⇧Back to the top](#java-style-guide)

#### Paragraphs

One blank line—that is, a line containing only the aligned leading asterisk (`*`)—appears between
paragraphs, and before the group of block tags if present. Each paragraph but the first has `<p>`
immediately before the first word, with no space after.

[⇧Back to the top](#java-style-guide)

#### Block tags

Any of the standard "block tags" that are used appear in the order `@param`, `@return`, `@throws`,
`@deprecated` and `@see`, and these five types never appear with an empty description. When a block
tag doesn't fit on a single line, continuation lines are indented four (or more) spaces from the
position of the `@`. The contents of the tags are always inline with the declaration.

  * `@param` Adds a parameter with the specified parameter-name followed by the specified
  description to the "Parameters" section. Only used on methods and classes and should be present
  always that the owning member has parameters. Every parameter should have its own tag definition

  ```java
  /**
   * javadoc description
   *
   * @param firstName the given name input by the user
   * @param lastName the surname input by the user
   */
   void populateUser(String firstName, String lastName) { ... }
  ```

  ```java
  /**
   * javadoc description
   *
   * @param T the object type the class is able to execute
   */
   class Executor<T> { ... }
  ```

  * `@return` Describes what the method returns. Only used on methods, and must be defined when
  the method is not `void`

  ```java
  /**
   * javadoc description
   *
   * @return an instance of User, with the default values for every property
   */
   User buildDefaultUser() { ... }
  ```

  * `@throws` Describes when an exception will be thrown by the owning method. Only used on
  methods and must be declared for every *checked* exception and optionally for *unchecked*
  exceptions

  ```java
  /**
     * javadoc description
     *
     * @throw ParseException when name doesn't follow the pattern '[A-Z][a-z]*'
     */
     void parseUserName() throws ParserException { ... }
  ```

  * `@deprecated` Describes the reason a member was deprecated, and ideally, informs if there is
  an alternative for replacing it. Mandatory for every deprecated member

  ```java
  /**
     * javadoc description
     *
     * @deprecated due to not including the {@code lastName} property in the result. Use
     *     {@link #formatFullUserName} instead
     */
     @Deprecated
     void formatUserName() { ... }
  ```

  * `@see` References links and other classes and methods that would be useful to the understanding
  of the owning member. It is never mandatory, and are added at the developer disclosure

  ```java
  /**
     * javadoc description
     *
     * @see http://somesite.com/how-parser-works
     * @see com.mycompany.Parser
     * @see com.mycompany.Parser#parseString
     */
     void parseUserName() { ... }
  ```

[⇧Back to the top](#java-style-guide)

### The summary fragment

Each Javadoc block begins with a brief **summary fragment**. This fragment is very important: it is
the only part of the text that appears in certain contexts such as class and method indexes.

This is a fragment—a noun phrase or verb phrase, not a complete sentence. It does **not** begin
with `A {@code Foo} is a...`, or `This method returns...`, nor does it form a complete imperative
sentence like `Save the record.`. However, the fragment is capitalized and punctuated as if it were
a complete sentence.

> **Tip:** A common mistake is to write simple Javadoc in the form
`/** @return the customer ID */`. This is incorrect, and should be changed to
`/** Returns the customer ID. */`.

[⇧Back to the top](#java-style-guide)

### Where Javadoc is used

At the *minimum*, Javadoc is present for every `public` class, and every `public` or `protected`
member of such a class, with a few exceptions noted below.

Additional Javadoc content may also be present, as explained in Section
[Non-required Javadoc](#non-required-javadoc).

  * **Exception:** *self-explanatory methods*: Javadoc is optional for "simple, obvious" methods
  like `getFoo`, in cases where there *really and truly* is nothing else worthwhile to say but
  "Returns the foo".

    > **Important:** it is not appropriate to cite this exception to justify omitting relevant
    information that a typical reader might need to know. For example, for a method named
    `getCanonicalName`, don't omit its documentation (with the rationale that it would say only
    `/** Returns the canonical name. */`) if a typical reader may have no idea what the term
    "canonical name" means.

  * **Exception:** *overrides*: Javadoc is not always present on a method that overrides a
  supertype method.

[⇧Back to the top](#java-style-guide)

#### Non-required Javadoc

Other classes and members have Javadoc as *needed or desired*.

Whenever an implementation comment would be used to define the overall purpose or behavior of a
class or member, that comment is written as Javadoc instead (using `/**`).

Non-required Javadoc is not strictly required to follow the formatting rules of section
[Where Javadoc is used](#where-javadoc-is-used), though it is of course recommended.

[⇧Back to the top](#java-style-guide)

[1]: https://google.github.io/styleguide/javaguide.html
[2]: http://docs.oracle.com/javase/tutorial/java/data/characters.html
[3]: https://blog.codinghorror.com/new-programming-jargon/
[4]: http://books.google.com/books?isbn=8131726592
[5]: http://checkstyle.sourceforge.net/
