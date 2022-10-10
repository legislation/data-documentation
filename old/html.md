# HTML Format

We provide the content of sections and tables of contents in a ready-transformed HTML format that is suitable for embedding within a web page. **These HTML snippets are only available through their [representation URI](/developer/uris#representations) and not through content negotiation.** The URI for an HTML snippet for a particular item of legislation can be identified through the `<atom:link>` with a title of `HTML snippet` within the XML or user-oriented HTML provided on the site.

The HTML snippets are wrapped in a `<div>` element with a class of `LegSnippet`. Many other classes are used within the HTML. Default stylesheets for these classes are available at:

*   [legislation.css](/styles/legislation.css)
*   [primarylegislation.css](/styles/primarylegislation.css) for primary legislation
*   [secondarylegislation.css](/styles/secondarylegislation.css) for secondary legislation
*   [legislation.css](/styles/legislation.css) for Northern Ireland Acts
*   [explanatoryNotes.css](/styles/explanatoryNotes.css) for Explanatory Notes

The HTML snippets include context information, such as the title of the Part that the section you're looking at belongs to.