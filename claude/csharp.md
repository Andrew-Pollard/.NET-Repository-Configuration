# C# and .NET

## Projects

- When contributing to an existing codebase, its conventions take precedence over everything in this file.
- Target the latest .NET, with `Nullable` and `ImplicitUsings` enabled and `<AnalysisLevel>10.0-all</AnalysisLevel>`.
  Builds must have no warnings.
- Name solutions, projects and folders `Invicta.<Area>` (`Invicta.Time`, `Invicta.Time.Tests`) and set
  `RootNamespace` to `Invicta`. Namespaces mirror the matching `System` namespace: a `TimeProvider` subclass goes
  in `Invicta`, threading types in `Invicta.Threading`. Folders match namespaces.
- Follow the prevailing folder structure of high-quality C# codebases: currently `src/`, `tests/`, `benchmarks/`
  and `samples/`, with an `.slnx` solution.
- No top-level statements: executables declare `internal static class Program` with a `private static Main`.
- Check style with `dotnet format --verify-no-changes --severity info`; a normal build doesn't report IDE
  suggestions such as the file header or naming.

## Code

- `.editorconfig` is authoritative for formatting and naming, including `_camelCase` private fields, `s_` static
  fields and explicit types instead of `var`.
- Every file starts with `// © <year> Andrew Pollard. All rights reserved.` and `// Licensed under the MIT License.`
- Access modifiers show intent, even inside internal types: `public` for what would be public API if the type were
  public (including interface implementations and P/Invoke declarations), `internal` for assembly plumbing, and
  `private` for everything else.
- Use private fields rather than private properties.
- Prefer `is null`, `nameof`, pattern matching, switch expressions and throw helpers such as
  `ArgumentNullException.ThrowIfNull`. Trust nullable annotations rather than adding redundant null checks.
- Asynchronous methods end in `Async`, except test and benchmark methods, whose names the runners display; public
  ones take a `CancellationToken` as their last parameter and pass it on.
  Avoid `async void` outside event handlers, never block on async code with `.Result` or `.Wait()`, and use
  `ConfigureAwait(false)` in library code.
- Suppress an analyzer finding only when it can't reasonably be fixed, with
  `[SuppressMessage("Category", "ID:Title", Justification = "…")]` on the narrowest member or type, or
  `[assembly: SuppressMessage(…)]` in `GlobalSuppressions.cs`. Never use `<NoWarn>` or `#pragma warning disable`.

## Blank lines and wrapping

Blank lines split code into paragraphs that can be skimmed by intent, such as "validate the arguments".

- A blank line goes either side of any member with a body, XML docs or attributes, or that spans several lines.
- Group single-line fields, constants and auto-properties by purpose, not by kind, with a blank line between groups.
  A backing field sits directly under its property.
- Argument validation comes first, one paragraph per argument, then a blank line.
- Leave a blank line after a closing brace, and before the final `return` unless it pairs with the line above.
- Split calculations into paragraphs of one to three lines per step.
- Keep a declaration attached to the statement that consumes it. A one-line operation stays attached to a simple
  check of its result; separate a multi-line call or complex check with a blank line.
- A `//` comment starts a paragraph: blank line above, code directly below.
- Group `using` directives by root namespace (`System`, `Microsoft`, third-party, `Invicta`), separated by blank lines.
- Put each `where` constraint on its own line, and a primary constructor's base list on the next line.
- The closing parenthesis stays on the line of the last argument or parameter.

## Comments and documentation

- Every non-test type and member, including internal and private ones, has `///` XML docs; fields and trivial
  private constructors may go without. Implementations of interface members can use `<inheritdoc/>`.
- Summaries start with a present-tense verb ("Gets…", "Creates…"). Boolean properties start "Gets a value
  indicating whether". Use `<see langword="null"/>` for keywords, and don't start exception docs with "Thrown if".
- Details that callers need go in `<remarks>`; notes for maintainers, such as rationale or "guarded by `_lock`",
  stay as `//` comments in the implementation.
- Public docs never `<see cref>` a private member; state the fact in prose instead.
- Trailing comments are a few words at most, such as units; anything longer goes on the line above.

## Tests

- Use NUnit with the constraint model (`Assert.That(actual, Is.EqualTo(expected))`), and NSubstitute only when
  something needs faking. Test projects reference `NUnit`, `NUnit3TestAdapter`, `NUnit.Analyzers` and
  `Microsoft.NET.Test.Sdk`.
- Test fixtures are `internal sealed class`, named `<Type>Tests` in folders mirroring the code under test. Tests are
  named `Method_Scenario_Expectation`.
- Group independent assertions in `using (Assert.EnterMultipleScope())`; use `[TestCase]` or `[TestCaseSource]`
  rather than near-duplicate tests.
- No "Arrange", "Act" or "Assert" comments, and no commented-out or ignored tests left behind.
- Put tests that depend on wall-clock timing in their own category, so they can be excluded on busy machines.
- Confirm the tests actually ran, from the test count, before reporting them passed.

## Native interop

- Follow Microsoft's [native interoperability best practices][interop]: `[LibraryImport]`, a class named after the
  DLL (`Kernel32`), native names for functions, parameters and constants, the closest native types, `SafeHandle` and
  `SetLastError = true`.
- Add `[DefaultDllImportSearchPaths(DllImportSearchPath.System32)]` to each import, and suppress IDE1006 on the
  class with a `[SuppressMessage]`.
- Each native function's XML docs end with `<seealso href="…"/>` linking to its official documentation.

[interop]: https://learn.microsoft.com/dotnet/standard/native-interop/best-practices
