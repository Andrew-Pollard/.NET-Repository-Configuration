<!--
Andrew Pollard's personal Claude Code instructions. ~/.claude/CLAUDE.md imports this file, so it applies to every
project; the C# and Markdown files are imported at the end. Keep the three files under about 200 lines in total.
-->

# Working with me

- IMPORTANT: never run `git commit` unless I asked for it in that message or confirmed it. The same applies to
  `git push`, amending, resetting and rewriting history. "Fix X and commit" is a request to commit; "fix X" is not.
- Make and verify changes, summarise what changed, then ask before committing.
- Answer every part of a multi-part request separately, so none is overlooked.
- Say what you verified and what you only expect. Show the evidence, such as the command you ran and its result,
  rather than just reporting success.
- Mention bugs, broken invariants or doubtful assumptions you notice, even outside the current task.
- Fix the root cause of warnings, errors and failing tests rather than suppressing them.

# Principles

- **Readability first:** split work into small, descriptively named methods rather than dense blocks of
  algorithmic code. Trading some performance for readability is fine while the code still meets its purpose;
  measure before choosing a denser, faster version.
- **Don't reinvent the wheel:** before building anything complicated, check whether it is already solved. Prefer the
  .NET base libraries, then reputable open-source libraries (Microsoft, Google and similar), then custom code, and
  say why when custom code is still needed.
- **Minimal:** no speculative features, options or abstractions.

# Language

- British English in long-form text: READMEs, documentation and commit messages.
- American English in code, code comments, XML docs, configuration file comments and code snippets in Markdown, to
  match .NET's own spelling.
- Where a .NET term reads oddly in British prose, such as "analyzers", rephrase it or name the type in code font.

# Git

- Prefer a new commit over amending one, and never force-push unless asked.
- When asked to commit and push, commit first, check the result, then push.

# Windows environment

- **Line endings:** repositories check out with CRLF (`core.autocrlf=true`; `.gitattributes` normalizes the index
  to LF). The Write tool creates LF files, so convert new files to CRLF without a BOM and check for LF or mixed
  endings before finishing. If `git status` then lists files whose diff is empty, run `git add -u`.
- **Commit messages:** Windows PowerShell 5.1 adds a BOM to text piped into `git commit -F -`. Write the message to
  a BOM-free file and run `git commit -F <file>`.

# New repositories

- Start from the Configuration repository (`C:\Users\Andrew\Documents\Claude\Configuration`): copy `.editorconfig`,
  `.gitattributes`, `.gitignore`, `LICENSE` (MIT) and `THIRD-PARTY-NOTICES.md`, and add a project-specific
  `exclusion.dic` for the spelling checker.

@csharp.md
@markdown.md
