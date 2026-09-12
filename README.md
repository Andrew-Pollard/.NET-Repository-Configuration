# Configuration

Shared `.editorconfig`, `.gitattributes` and `.gitignore` for new repositories.

## `.editorconfig`

From [dotnet/runtime v10.0.0][runtime-editorconfig].

- **Whitespace:** 4 spaces for C#, 2 for project, XML, JSON and YAML files; a final newline; no trailing
  whitespace. `.sh` files are LF, `.cmd` and `.bat` are CRLF.
- **Types:** explicit types rather than `var`, reported as a warning; language keywords (`int`, `string`)
  rather than BCL type names.
- **Naming:** `s_` for static fields, `_camelCase` for private and internal fields, PascalCase for constants.
- **Layout:** file-scoped namespaces, `using` directives outside the namespace with System first, braces on
  their own line and around every block.
- **Header:** `// © 2026 Andrew Pollard. All rights reserved.`
- **Guides:** ruler hints at 80 and 120 columns, for the Visual Studio guidelines extension.

> [!NOTE]
> `spelling_exclusion_path` points at `exclusion.dic` in the repository root, which is not included here
> because its contents are project-specific. Add one per repository listing the words the Visual Studio spell
> checker should ignore, one per line.

## `.gitattributes`

Combines the [Common][common-gitattributes], [C#][csharp-gitattributes], [Markdown][markdown-gitattributes],
[Visual Studio][visualstudio-gitattributes] and [Visual Studio Code][vscode-gitattributes] templates.

- **Line endings:** text files are normalised to LF in the repository.
- **Windows tooling:** `.sln`, `.slnx`, `.csproj`, `.props`, `.bat`, `.cmd` and `.ps1` are checked out as CRLF.
- **Binary types:** marked so Git does not try to diff or merge them.

## `.gitignore`

Combines the GitHub [Windows][windows-gitignore], [Visual Studio][visualstudio-gitignore] and
[Visual Studio Code][vscode-gitignore] templates.

- **Build output:** `bin/`, `obj/`, `[Dd]ebug/`, `[Rr]elease/` and `artifacts/`.
- **Results:** test, coverage and BenchmarkDotNet output.
- **NuGet packages:** `*.nupkg` and `packages/`.
- **Editor and user files:** `.vs/`, `*.user`, `*.suo`, and `.vscode/` apart from a few shared settings files.
- **Windows shell files:** `Thumbs.db`, `desktop.ini` and `*.lnk`.

[runtime-editorconfig]: https://github.com/dotnet/runtime/blob/v10.0.0/.editorconfig
[common-gitattributes]: https://github.com/gitattributes/gitattributes/blob/master/Common.gitattributes
[csharp-gitattributes]: https://github.com/gitattributes/gitattributes/blob/master/CSharp.gitattributes
[markdown-gitattributes]: https://github.com/gitattributes/gitattributes/blob/master/Markdown.gitattributes
[visualstudio-gitattributes]: https://github.com/gitattributes/gitattributes/blob/master/Global/VisualStudio.gitattributes
[vscode-gitattributes]: https://github.com/gitattributes/gitattributes/blob/master/Global/VisualStudioCode.gitattributes
[windows-gitignore]: https://github.com/github/gitignore/blob/main/Global/Windows.gitignore
[visualstudio-gitignore]: https://github.com/github/gitignore/blob/main/VisualStudio.gitignore
[vscode-gitignore]: https://github.com/github/gitignore/blob/main/Global/VisualStudioCode.gitignore
