
# HTML

## XHTML snippets

We provide the content of items, sections and tables of contents in a ready-transformed XHTML format that is suitable for embedding within a web page. **These HTML snippets are only available through their [representation URI](/model/uris/reference.md#representation-uris) and not through content negotiation.** 

The XHTML snippets use the exact same HTML markup as the content pane of our website. The markup is wrapped in a `<div>` element with a class of `LegSnippet`. Many other classes are used within the HTML. Default stylesheets for these classes are available at:

*   [legislation.css](https://www.legislation.gov.uk/styles/legislation.css)
*   [primarylegislation.css](https://www.legislation.gov.uk/styles/primarylegislation.css) for primary legislation
*   [secondarylegislation.css](https://www.legislation.gov.uk/styles/secondarylegislation.css) for secondary legislation
*   [legislation.css](https://www.legislation.gov.uk/styles/legislation.css) for Northern Ireland Acts
*   [explanatoryNotes.css](https://www.legislation.gov.uk/styles/explanatoryNotes.css) for Explanatory Notes

The HTML snippets include context information, such as the title of the Part to which the section you’re looking at belongs.

You can get an item or section as an XHTML snippet by appending `/data.xht` to a version URI.

## HTML5

We provide the content of items and sections in a ready transformed HTML5 format. The HTML5 files are self-contained and link to CSS stylesheets that provide appropriate styles for the content, so you can display them on their own.

If you request a section of an item of legislation as HTML5, the content will also include context information, such as the title of the Part to which that the section you’re looking at belongs.

You can get an item or section as HTML5 by appending `/data.html` to a version URI.

## Large documents

Some items of legislation are very large and therefore take a long time for legislation.gov.uk to retrieve and transform into HTML. **We recommend avoiding requesting entire items of legislation as HTML.**
