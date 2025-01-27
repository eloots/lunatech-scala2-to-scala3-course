# Opaque Type Aliases

> NOTE: this exercise is optional. It's purpose is to show that certain use
>       cases of opaque type aliases sound great at first, but turn out
>       to be very difficult to implement

## Background

An Opaque Type Alias can be used to provide the functionality of a "wrapper
type" (i.e. a type that wraps, and therefore hides, another type) but without
any runtime overhead. The aim is to provide additional type-safety at
compile-time but then be stripped away at runtime. It is a powerful new feature
of Scala 3 for supporting Information Hiding.

Opaque Type Aliases differ from plain Scala 2 Type Aliases in that the later
just provide a new name for a type but wherever this new name is used, the
call-site still knows the details of the original type being aliased. With
Opaque Type Aliases, the original type being aliased is hidden (or is opaque) at
the call-site.

## Steps

- Open the `TopLevelDefinitions.scala` file that you created during the exercise
  on Top-Level Definitions. Here you should see a few type aliases that were
  created to help with the readability of the code.

```scala
...
type CellContent = Set[Int]
type ReductionSet = Vector[CellContent]
type Sudoku = Vector[ReductionSet]

type CellUpdates = Vector[(Int, Set[Int])]
...
```

To keep things manageable we will only focus on one of these type aliases for
this exercise. Specifically we will convert the last of these type aliases,
`CellUpdates` into an Opaque Type Alias.

- To do that, simply add the keyword `opaque` in front of the type alias
  declaration and recompile. Do you expect this to compile successfully? If not,
  why?

- Use your experience from the exercise on Extension Methods to fix the
  compilation errors of the form `value {name} is not a member of
  org.lunatechlabs.dotty.sudoku.CellUpdates`
    - Tip: Fix all of the compilation errors of this form `value {name} is not a
      member of ...` before tackling the other types of error like `Found: ...
      Required: ...`
    - Tip: Some of the mission members for our new opaque type are generic (i.e.
      type-parameterised) methods. Do not be afraid to implement extension
      methods that are non-generic (i.e. without type-parameters), which might
      mean modifying existing call-sites.

- Now that we have added the necessary extension methods we still have to fix
  the remaining errors where we have a value of type `Vector[(Int, Set[Int])]`
  but the compiler is expecting the opaque type `CellUpates`
    - Tip: This is the point where we have to think how do we _get_ values of
      our opaque type
    - Tip: In general, an opaque type goes well together with a companion
      object.

- Note: Fixing one type of error (e.g. `Found: ... Required: ...`) may reveal
  new errors of type `value {name} is not a member of ...`. If that happens, it
  is generally easier to first fix the error of type `value {name} is not a
  member of ...` by adding an extension method, and then continue with the other
  type of error.

- Once all the compilation errors are fixed, run the provided tests by executing
  the `test` command from the `sbt` prompt and verify that all tests pass

- Verify that the application runs correctly

### Next steps

After successfully completing the tasks in this exercise, move to the next one by
running the `cmtc next-exercise` from the command line.

## Source code formatting & Markdown viewer in IntelliJ

### Source code formatting

[scalafmt](https://github.com/scalameta/scalafmt) based source code formatting is
in place in this project. scalafmt supports both Scala 2 and Scala 3. You can
[re]format the code by running `scalafmtAll` from the sbt prompt. As we switch from
Scala 2 to Scala 3, you need to make sure that a matching scalafmt configuration is
in place. In any of the exercises, you can run `cmtc pull-template .scalafmt.conf`
to "pull-in" the correct configuration file.

### Markdown viewer in IntelliJ

The font size can be a bit too small for the taste of some people. You can change the
Markdown zoom setting in IntelliJ by pasting the following CSS snippet in the
markdown setting in _" Settings" -> "Languages & Frameworks" -> "Custom CSS -> CSS rules"_
and adjust the font-size setting to your liking:

```
body {
  font-size: 120% !important;
  }
```

![IntelliJ Markdown viewer settings](images/Markdown-viewer-IntelliJ.png)
