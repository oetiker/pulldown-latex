# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

# [0.8.0] - 2026-07-27

## Added

- Added support for the `\mathord`, `\mathop`, `\mathbin`, `\mathrel`,
    `\mathopen`, `\mathclose`, `\mathpunct`, and `\mathinner` atom-class
    commands.
- Added support for the `\overbracket`, `\underbracket`, `\buildrel`,
    `\substack`, and `\sideset` stacking commands. `\sideset` currently parses
    the side scripts but renders only its base operator.
- Added all 68 case-sensitive `dvipsnames` colors from `xcolor` to `\color`,
    `\textcolor`, and the other color commands.
- Added the `\textrm`, `\textbf`, `\textit`, `\textsf`, and `\texttt`
    text-mode font selectors inside math mode. Font state now also styles
    `\text` content in MathML output.
- Added double-struck italic support through `\mathbbit` and `\symbbit`.
- Added `\strut` and the MathJax-compatible `\Space{width}{height}{depth}`
    command.
- Added fuzz targets for the parser, MathML renderer, input-complexity checks,
    and comparisons with KaTeX, together with CI coverage for building them.
- Expanded and reorganized the integration, font, MathML, and cross-browser
    test suites.

## Changed

- __Breaking Change__: `Event::Space` gained a `depth` field so renderers can
    represent spacing below the baseline.
- __Breaking Change__: `Font` gained the `BoldSymbol` and
    `DoubleStruckItalic` variants. Downstream exhaustive matches must handle
    both variants.
- `\kern`, `\hskip`, `\mkern`, and `\mskip` now accept dimensions or glue
    wrapped in a single brace group for compatibility with KaTeX and MathJax.
- Macro expansion is now limited to a depth of 64 and 1 MiB of allocated
    expansion text to prevent infinite recursion and memory exhaustion.
- The MathML renderer now recovers from malformed or unbalanced event streams
    and cleans up its open renderer state instead of panicking.

## Fixed

- Fixed unbraced command arguments consuming an entire run of digits; for
    example, `\frac12` is now parsed as `\frac{1}{2}`.
- Fixed HTML special characters in `\text` output not being escaped.
- Fixed `\boldsymbol` rendering: Latin letters and lowercase Greek use bold
    italic, while capital Greek and digits use bold upright.
- Fixed `\mathup` and `\symup` selecting the calligraphic font instead of the
    upright font.
- Fixed crashes caused by backslashed multibyte characters, unclosed
    environments, unexpected alignment or newline events, invalid macro
    parameters, out-of-bounds suffix scans, and error spans crossing UTF-8
    character boundaries.

# [0.7.1] - 2024-11-18

## Added

- Added support for `equation` and `equation*` environments.

# [0.7.0] - 2024-10-10

## Fixed

- Fix comments parsing inside of environments and groups.
- `\hline` and `\hdashline` before any content in a math environment.

## Changed

- __Breaking Change__: `Event::Alignment` and `Event::NewLine` were moved to
    `Event::EnvironmentFlow(EnvironmentFlow::Alignment)` and
    `Event::EnvironmentFlow(EnvironmentFlow::NewLine)` respectively.

## Added

- Added the `Event::EnvironmentFlow(EnvironmentFlow::StartLines)` variant, for when the first thing in the environment
    is a `\hline`/`\hdashline`.

# [0.6.3] - 2024-09-04

## Added

- The `Token` and `MacroSuffixNotFound` error variants.

## Fixed

- Fix comments parsing.

## Removed

- Removed the `ErrorKind::EndOfInput` variant in favor of more descriptive ones.

# [0.6.2] - 2024-09-02

No notable changes.

# [0.6.1] - 2024-08-31

## Fix

- Fix the `mathml` output when `annotation` is set.
- Fix the error display having asymmetric lines.

# [0.6.0] - 2024-08-27

## Added

- Robust CI setup.
- Miscellaneous documentation improvements.
- Errors are now pretty :)

## Changed

- Use criterion for benchmarks.
- Set MSRV to 1.74.1. (__Breaking Change__)
- The Dimension `type` is now a `newtype`, and is more ergonomic. (__Breaking Change__)
- The `ColorChange` event changed to be smaller in memory. (__Breaking Change__)

## Fixed

- Array rendering with custom line spacing.
- Expansion spans being to eagerly popped.
- Benchmark errors and doc-tests not compiling.

## Removed

- Dependency on `thiserror`.

# [0.5.1] - 2024-08-02

## Changed

- Made the demo site look somewhat good.

## Fixed

- Fix `\phi` and `\varphi` being inverted.
- Fix spacing in mathematical environments rows.

# [0.5.0] - 2024-08-02

## Changed

- Small documentation improvements.

## Added

- A usage section in the crate documentation.

## Removed

- Made `InnerParser` private. (__Breaking Change__)
- Made `MacroContext` private.  (__Breaking Change__)

# [0.4.0] - 2024-08-01

## Changed

- Added a full error trace to the errors returned by the `Parser`.
- Updated `fantoccini` from `0.19.0` to `0.21.0` in test suite.
