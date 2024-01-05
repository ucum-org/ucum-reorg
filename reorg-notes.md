# Notes regarding the reorganization of UCUM spec

This work was performed in January 2024 as part of a larger effort to modernize and streamline the UCUM standard for greater acceptance.

All effort has been made to not change the meaning of the specification. Rather, minor formatting and organization changes have been made with the goals of consistency, clarity, and adherence to Markdown formatting.

The single largest modification is the extraction of units/prefixes from the documentation. This was done to keep each distinct, allowing for more reliable change management and clarity.

As there are numerous "flavors" of Markdown, GitHub-flavored Markdown (GFM) is the target for any styling.

Notable changes:
- Repeated use of "The Unified Code for Units of Measure" has been shortened to UCUM after the acronym is introduced in the head of the document.
- Mixed use of numbered headings, sections, and numbered reference points have been eliminated in favor of a single system of numered headings with numbered lists. Specific points can still be referenced in this new system.
- In the original XML spec, `<code>` tags were used to distinguish units and other technical pieces. These have been replaced with the standard Markdown use of backticks (`).
- Numerous organization names and standards were distinguished with `<emph>` (i.e. italics). These have been largely replaced in favor of links to organization websites or other source information.
- Typos corrected throughout.

Questions and concerns for future consideration:

1. Use of 7-bit ASCII prevents use of many non-English characters as arbitrary units. UTF-8 is now accepted as the default. We do need to consider any downstream consequence of using multibyte characters.
2. Footnotes are not used in the traditional sense for citations but for commentary. The first footnote seems petty and unnecessary. There are other examples of seemingly unnecessary commmentary throughout the spec.
3. There are references wrapped in square brackets, e.g. references to ISO/ANSI spec. I suggest changing these to footnotes and eliminating commentary-based footnotes or changing their nature to fit.
4. Rather than include various alphabetic listing of units, I advise the use of a "browser" which allows the units to be sorted at the user's request.