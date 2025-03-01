# Doxygen Commands

Include a limited set of Doxygen commands in parsed Markdown.

Swift Markdown includes an option to parse a limited set of Doxygen commands, to facilitate
transitioning from a different Markdown parser. To include these commands in the output, include
the options ``ParseOptions/parseBlockDirectives`` and ``ParseOptions/parseMinimalDoxygen`` when
parsing a ``Document``. In the resulting document, parsed Doxygen commands appear as regular
``Markup`` types in the hierarchy.

## Parsing Strategy

Doxygen commands are written by using either a backslash (`\`) or an at-sign (`@`) character,
followed by the name of the command. Any parameters are then parsed as whitespace-separated words,
then a "description" argument is taken from the remainder of the line, as well as all lines
immediately after the command, until the parser sees a blank line, another Doxygen command, or a
block directive. The description is then parsed for regular Markdown formatting, which is then
stored as the children of the command type. For example, with Doxygen parsing turned on, the
following document will parse three separate commands and one block directive:

```markdown
\param thing The thing.
This is the thing that is modified.
\param otherThing The other thing.

\returns A thing that has been modified.
@Comment {
    This is not part of the `\returns` command.
}
```

Doxygen commands are not parsed within code blocks or block directive content. No indentation
adjustment is performed on paragraph arguments that span multiple lines, unlike with block directive
content.

## Topics

### Commands

- ``DoxygenParam``
- ``DoxygenReturns``

<!-- Copyright (c) 2023 Apple Inc and the Swift Project authors. All Rights Reserved. -->
