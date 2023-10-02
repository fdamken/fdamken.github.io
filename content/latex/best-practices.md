---
title: "LaTeX Best Practices"
draft: true
---

I use LaTeX a lot.
And every time I work with other people, I notice things people to weirdly when using LaTeX, not pushing it to its full potential or simply doing things that are “dangerous.”
Of course, not dangerous in the sense of physically hurting anybody, but in risking a non-robust document, weird typesetting, or simply an unpleasant document.
Thus, I decided to collect this list of “best practices” so that I can refer to it and, of course, to make these things more well-known.

If you want to contribute, [feel free to create an issue](https://github.com/fdamken/fdamken.github.io/issues/) or [submit a pull request](https://github.com/fdamken/fdamken.github.io/pulls).
Thanks to [Heiko](https://miterion.de/) who helped extending this list.

Note that this is a bit different from my [LaTeX tips & tricks]({{< relref "latex/tips-and-tricks" >}}) and a lot more basic, although I will refer to said page from time to time.

But even with these best practices, remember:
> You cannot use LaTeX correctly. Use can just use it less wrong.


## Best Practices
### General
1. Compile your document with as few warnings as possible as they actually tell you useful information about your document. Use [`silence`](https://www.ctan.org/pkg/silence/)‘s `\WarningFilter` if you want to ignore specific warnings to get a cleaner output. [Go to full explanation.](#compile-with-as-few-warnings-as-possible)
2. Use an acronym package to automatically introduce acronyms appropriately. Use [`acronym`](#handling-acronyms-acronym) if you just need the handling (for small documents such as papers) and [`glossaries`](#handling-acronyms-glossaries) if you need a glossary (for large documents such as theses).
3. Format your source code. Even though LaTeX is not a programming language (yes, it is Turing complete, no, that does not qualify it as a programming language), it is still vital that the document is maintainable. [Go to full explanation.](#code-formatting)
4. Read documentation. Most packages have an excellent and extensive written documentation that contains everything you might need. Check out, for instance, the documentation of [`glossaries`](https://ctan.mirror.rafal.ca/macros/latex/contrib/glossaries/glossaries-user.pdf) and [`glossaries-extra`](https://ctan.mirror.globo.tech/macros/latex/contrib/glossaries-extra/glossaries-extra-manual.pdf). It is extensive (combined, 1766 pages), and extremely well-written.
5. Use [`todonotes`](https://ctan.org/pkg/todonotes) and `\todo` to denote todos in the document. If your document class does not have wide margins, put `\setuptodonotes{inline}` in the preamble.
6. **Never** allow compilation errors to persist in your document. If you are using Overleaf, change `Try to compile despite errors` to `Stop on first error` in the menu next to the `Recompile` button to remind you of this. [Go to full explanation.](#never-allow-errors-to-persist)
7. Do a clean compile (i.e., delete all auxiliary files) from time to time to check everything is working. Even better, set up continuous integration.
8. Use a build tool such as [`arara`](https://islandoftex.gitlab.io/arara/) or [`latexmk`](https://mg.readthedocs.io/latexmk.html) for building large documents to prevent forgetting crucial steps (e.g., generating glossaries, running BibLaTeX, etc.). Makefiles might also work for small documents.
9. Know the difference between `\input` and `\include`, and use both of them appropriately. [Go to full explanation.](#difference-between-input-and-include)
10. Instead of formatting dates and times manually, use `datetime2`. It respects the language and locale of the document and ensures consistent formatting.

### General Typesetting
1. Handle inter-word and inter-sentence spaces correctly. Use `\ ` and `\@` if necessary. [Go to full explanation.](#handling-inter-word-and-inter-sentence-spaces)
2. Know the difference between hyphen (-), en- (--) and em-dash (---) and use all three appropriately. [Go to full explanation.](#hyphen-en-and-em-dash)
3. Decide whether to reference equations every time (and treat them like non-floating figures) or embedding them into the text (treating them as inline math). In any case, be consistent (and respect the journal‘s guidelines).
4. Configure custom hyphenation for words unknown to `babel` if necessary.
5. [Use `csquotes` for placing quotation marks.]({{< relref "latex/tips-and-tricks" >}}#automatically-using-correct-quotation-marks) Only use `"` and `'` in the code, never `‚`, `‘`, `’`, `„`, `“`, `”`, or similar.
6. Use `\textsuperscript` and `\textsubscript` for super- and subscripts within text, respectively. Do not use ‘sppontaneous math mode.’
7. Use `\emph` instead of `\textit`, `\textbf`, or similar for emphasizing. `\emph` is made for emphasizing, can be configured globally, and _toggles_ the font style rather than setting it (i.e., withing an italic text, emphasized words will become straight).
8. Place a `~` between `\cite` and the previous word to produce a no-break blank (i.e., a blank where no line break will take place). Otherwise, teh citation might be on the next line which looks weird.
9. Use `microtype` for microtypography (protrusion and expansion). It enhances your document a lot while being barely noticable.

### Layouting
1. Do not ignore over-/underfull h-/vbox warnings. That warning is _literally_ telling you that your document looks shitty somewhere. [Go to full explanation.](#do-not-ignore-over-underfull-hbox-and-vbox-warnings)
2. Touch layouting only if absolutely necessary. Avoid `\vspace`, `\hspace`, `minipage`, etc. In almost all cases, LaTeX knows what it is doing and you should rather adjust text length/figure size/etc. to get the desired result.

### Math
1. Do not use `\frac` in text/inline math mode. It gets too compressed, increases the line height, and makes the document look horrible. Instead, simply use a `/`.
2. Use `\prescript` (or so) instead of `^2T_1`; the latter binds to the wrong symbol
3. Do not use `^2T_1` and similar to typeset `²T₁`, instead use `\prescript{superscript}{subscript}{arg}` for super-/subscripts before a symbol, e.g., `\prescript{2}{}{T}_1`. [Go to full explanation.](#use-prescript)
4. Be aware of cool features such as `\underbrace`, `\mathclap`, `\phantom`, etc. [Go to full explanation.](#cool-math-features)
5. (Debatable) Prefer `\( … \)` over `$ … $` and prefer `\[ … \]` over `$$ … $$`. The dollar notation is a TeX primitive and not meant to be used in LaTeX documents.
6. Use `\DeclareMathOperator` rather than retyping an operator over and over again as this is prone to induce typos. [Go to full explanation.](#use-declaremathoperator)
7. Use `siunitx` for units, numbers, ranges, uncertainties, etc. [Got to full explanation.](#use-siunitx-for-units)
8. Use `physics` package for easier calculus and all kinds of physics typesettings. [Go to full explanation.](#use-physics-package)
9. Do not use `\text` for “operators,” instead use `\mathrm`. Example: Use `\( D_\mathrm{KL} \)`, not `\( D_\text{KL} \)`. [Go to full explanation.](#do-not-use-text-for-operators)
10. Use left/right versions of symbols, e.g., `\lvert` and `\rvert` instead of `\vert` whenever semantically reasonable. [Go to full explanation.](#use-leftright-versions-of-symbols)
11. Use `mathtools` instead of plain `amsmath` as it fixes lots of `amsmath`‘s bugs and adds extra functionality.
12. Do not rely on paranthesis auto-scaling (`\left` and `\right`), it looks horrible most of the time as the scaling is quite primitive. Instead, use `\big`, `\Big`, `\bigg`, and `\Bigg` and their respective left/right versions `\[lr]big`, `\[lr]Big`, `\[lr]bigg`, and `\[lr]Bigg`. [It is also possible to create bigger versions.](https://tex.stackexchange.com/a/6796/)
13. Do not use “plain symbols” such as `||`/`...`/etc.. Instead use `\Vert`/`\dots`/etc. [Go to full explanation.](#do-not-use-plain-symbols)
14. Do not use `\[ … \]` or `$$ … $$`, use an `equation` environment instead.
15. know the differences between `equation`, `gather`, and `align`

### Referencing
1. Label equations only when they are references. [This can be done automatically.]({{< relref "latex/tips-and-tricks" >}}#only-number-referenced-equations)
2. Do not use plain `\ref`s, use `cleveref` and `\cref` or at least `\autoref`. [Go to full explanation.](#do-not-use-plain-ref)

### Figures
1. Figures belong in `figure` environment, tables in `table` environments, listings in the respective listing environment, etc. [Go to full explanation.](#figure-placement)
2. Never place figures within text, they should _float_ to the top (or bottom) of the page. Let LaTeX handle this. [Go to full explanation.](#figure-placement)
3. Figures, tables, algorithms, listings, etc. are _floating_ objects. Do not enforce figure placement, LaTeX knows what it is doing. [Go to full explanation.](#figure-placement)
4. If a small image is tightly bound to a piece of text and does not carry meaning in itself, it is not a figure. Place it in a `center` environment and keep it where it is.
5. Center captions if they are below one line long and left-align them if they are more than one line long. Do so by adding `\captionsetup{singlelinecheck=on}` in the preamble.

### Tables
1. Use `booktabs` instead of standard tabulars. [Go to full explanation.](#use-booktabs)
2. Use `threeparttable` to add notes to a table (similar to footnotes in normal text, but withing the floating environment). [Go to full explanation.](#use-threeparttable-for-notes)
3. Use `siunitx` for formatting numbers in tables (such that they align at the decimal point, the uncertainty, or both). [Go to full explanation.](#use-siunitx-for-tables)


## Full Explanations
Some of the above items need a longer explanation, which is contained in this section.
Note that this section does not contain all best practices and for an exhaustive read, go [here](#best-practices).

### General
#### Compile With as Few Warnings as Possible
TODO

#### Handling Acronyms: `acronym`
TODO

#### Handling Acronyms: `glossaries`
TODO

#### Code Formatting
TODO

#### Never Allow Errors to Persist
TODO

#### Difference Between Input And Include
TODO

### General Typography
#### Handling Inter-Word And Inter-Sentence Spaces
TODO

#### Hyphen, En-, and Em-Dash
TODO

### Layouting
#### Do Not Ignore Over-/Underfull `hbox` And `vbox` Warnings
TODO

### Math
#### Use `\prescript`
Classic super- and subscript, i.e., `^` and `_`, bind to the symbol before them such that `A ^1T_2` would be rendered as `A¹ T₂`, not `A ¹T₂`.
`\prescript` is from the `mathtools` package and there are other packages available that do a similar thing, but `mathtools` is often loaded anyways.

#### Cool Math Features
TODO

#### Use `\DeclareMathOperator`
TODO

#### Use `siunitx` For Units
TODO

#### Use `physics` Package
TODO

#### Do Not Use `\text` For Operators
Using `\text` changes the font family to the document’s text family while `\mathrm` retains the math font but removes spacing that would otherwise be placed between letters.
Note that for actual text, `\text` can still be used and `\mathrm` removes all spaces (which should never be used in math operators anyway).

#### Use Left/Right Versions of Symbols
TODO

#### Do Not Use Plain Symbols
TODO

### Referencing
#### Do Not Use Plain `\ref`
TODO

### Figures
#### Figure Placement
TODO

### Tables
#### Use `booktabs`
TODO

#### Use `threeparttable` For Notes
TODO

#### Use `siunitx` For Tables
TODO


## Notes
This is an unstructured list of things that will be added to list of best practices, but they are not yet formulated well enough.
For completeness and transparency, I will keep them here.
- a multi-line equations that should get a single number should be an `aligned` environment inside one `equation`
- prefer `tikzplotlib` over `pgf` over `pdf` over `png` when building figures
	- really never use `png`
	- `tikz` renderings can be cached to speedup compilation time
- place every sentence on a new line to make finding compiler errors easier (opinionated)
- `\/`
- Use the biblatex package with the Biber backend instead of natbib (or even bibtex directly)
- use xspace for proper spacing after a stop
- Typeset numbers in math font (using siunitx) off they are ‘technical.’ E.g., `we used a learning rate of \num{0.12} and we are 14 people in our lab.``
- Know that you can tell latex to just compile some `\includes` while still reading the aux file for labels, saving a ton of compilation time during writing
- don't define labels multiple times (ideally create labels in the moment you want to reference them)
- make sure no figures is left unreferences
- make sure no unresolved references remain (**read the warnings**)
- whenever you feel like you need a `[vh]space`, think again; you probably do not need it
	- want to space out two parts of an equation? use align
    - `\quad` and `\qquad` are also great alternatives to provide typographically sound spacing
- use linewidth not textwidth
