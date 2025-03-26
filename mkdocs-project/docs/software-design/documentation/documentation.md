# TSTool / Software Design / Documentation #

TSTool software has significant developer and user documentation.

*   [Markdown/MkDocs Documentation](#markdownmkdocs-documentation)
*   [Legacy Word/PDF Documentation](#legacy-wordpdf-documentation)

----------------------

## Markdown/MkDocs Documentation ##

TSTool documentation was migrated to from Word/PDF to Markdown/MkDocs in early 2018 and is available in the following repositories.

*   [User Documentation](https://github.com/OpenCDSS/cdss-app-tstool-doc-user)
*   [Developer Documentation](https://github.com/OpenCDSS/cdss-app-tstool-doc-dev)

The Markdown/MkDocs documentation is now the standard documentation and the legacy documentation discussed
in the next section is being phased out.  MkDocs creates a static HTML website from Markdown,
with nice theme-based formatting, search, and navigation.
Any web browser can be used to view the documentation.

TSTool command editors and ***Help*** menu display software documentation by calling a web browser
with OpenCDSS documentation URLs.
TSTool attempts to show documentation for the current software version and if that fails it uses documentation from "latest".

## Legacy Word/PDF Documentation ##

Legacy user documentation was created in Word format and manually saved to PDF from Word,
saved in the following repository:

*   [cdss-app-tstool-doc](https://github.com/OpenCDSS/cdss-app-tstool-doc)

This documentation has been moved to Markdown and is retained only for archival purposes.

Each file uses header and other styles that allow a table of contents to be created.
However, automating conversion of Word to PDF is not straightforward
(at least it was not when the procedure was put in place and given the need to focus resources
on technical work to enhance the software features).
Consequently, PDF files are committed to the repository and a custom Java program
that uses [iText](https://itextpdf.com/).
However, this tool has never been released publicly and is not integrated into the TSTool repositories.
The legacy approach should generally not be needed now that TSTool user documentation has
been migrated to Markdown/MkDocs.
If Word/PDF needs to be processed, current PDF automation tools could be used or the
PDF tool could be made available (not a high priority).
