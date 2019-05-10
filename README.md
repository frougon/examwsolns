# examwsolns — Typesetting solutions with the `exam` class

The `examwsolns` package provides a `wsolution` environment for the
`exam` LaTeX document class. This environment can automatically adapt
the produced `mdframed` frame to its context (outer, question, part,
subpart or subsubpart).

## Package options

The `examwsolns` package accepts only one option:
`replace-solution-env`. Using it as `replace-solution-env` or as
`replace-solution-env=true` is equivalent. The default is `false`. When
`true`, it tells `examwsolns` to redefine the `solution` environment to
be identical to `wsolution`.

Package options (well... *the* option) can also be specified with:

    \examwsolnsSetup{<options>}

For `replace-solution-env`, this only has effect if done in the preamble
(the `solution` environment is redefined from the `\AtBeginDocument`
hook in order to avoid problems due to package loading order).

## The `wsolution` environment

### Question level

The `wsolution` environment takes two optional arguments. If the first
argument is passed and non-empty, it must be an integer in the [0, 4]
range and gives the amount of indentation (and thus the width) of the
produced `mdframed`;

  - if the value 0 is used, the frame starts at the left margin (what we
    call `outer` level);
  - the value 1 corresponds to the `question` level;
  - the value 2 corresponds to the `part` level;
  - the value 3 corresponds to the `subpart` level;
  - the value 4 corresponds to the `subsubpart` level.

If this first argument is omitted or blank, the `wsolution` environment
takes appropriate indentation and width for the current question level
(which can be any of the five aforementioned levels).

### Options passed to the `mdframed` environment

The `mdframed` environment is passed the `leftmargin` parameter
according to what we just explained, plus additional parameters that
are:

  - those from the `wsolution` environment's second argument if
    provided;
  - else, have been specified with the closest
    `\examwsolnsSetMdFramedDefaultArgs` command according to TeX's
    grouping rules (this command takes one argument: tokens to pass as
    additional options to `mdframed`);
  - none if the `wsolution` environment has been used with no second
    argument and `\examwsolnsSetMdFramedDefaultArgs` hasn't been called
    in an accessible scope.

### Pre-text and post-text inside `mdframed`

The contents of a `wsolution` environment becomes the contents of an
`mdframed` environment, except that you can have automatic pre-text and
post-text inserted. For example, if you say
`\examwsolnsSetMdFramedPreText{pre-text:}`,
`\examwsolnsSetMdFramedPostText{:post-text}` and use, in a scope
where these definitions are visible:

    \begin{wsolution}Solution text\end{wsolution}

then the `mdframed` environment (if printed) will have
`pre-text:Solution text:post-text` as its contents.
`\examwsolnsSetMdFramedPreText` and `\examwsolnsSetMdFramedPostText`
obey TeX's scoping rules (they respect groups), just like a `\def`
command. When used, the `\examwsolnsSetMdFramedPreText` and
`\examwsolnsSetMdFramedPostText` commands override the default values
defined in `examwsolns.sty`. These default values are equivalent to
doing:

    \examwsolnsSetMdFramedPreText{%
      \textbf{Solution:}\enspace \ignorespaces}

and

    \examwsolnsSetMdFramedPostText{\unskip}

### Showing or hiding answers

`wsolution` environments are ignored unless the `answers` option has
been passed to the `exam` class (in other words, the `wsolution`
environment respects the `\ifprintanswers` conditional).

## The five indentation amounts

The indentation amount from the left margin corresponding to each of the
five question levels are accessible via the following `〈dimen〉`
parameters: `\examwsolnsOuterIndent`, `\examwsolnsQuestionIndent`,
`\examwsolnsPartIndent`, `\examwsolnsSubpartIndent` and
`\examwsolnsSubsubpartIndent`.

## About the `examwsolns` package

The `examwsolns` package was written to answer [this TeX.SE
question][question]. You can find a sample `.tex` file showing to use
it and corresponding screenshots in [that answer][answer] (see also the
`examples` subdirectory here).

## License

The `examwsolns` package is distributed under the conditions of the LaTeX
Project Public License, either version 1.3 of this license or (at your
option) any later version. See examwsolns.sty for the precise licensing
information.

  [question]: https://tex.stackexchange.com/questions/489374/exam-creating-a-solution-environment-whose-width-is-set-by-an-optional-argument
  [answer]: https://tex.stackexchange.com/a/489424/73317
