V2
---------------------------------------------------------------------------------------
Prompt 1.1
-----------------------------------------------------------------------------
# DocuLens — Professional Comparison, Search Highlighting & Header Upgrade

Act as a senior product engineer, document intelligence engineer, and UX designer. Improve my existing DocuLens application for public use.

This is an existing React + TypeScript + Vite project. Inspect the repository, current components, types, services, PDF parsing, search, comparison engine, storage, and styles before making changes.

**Do not replace the application with a new project. Do not make unnecessary database, IndexedDB, storage-format, or architecture changes. Preserve existing functionality and documents.**

## 1. Product identity and logo

Use the existing DocuLens logo from:

https://github.com/Devputta/Drafts-might-be-needed-/blob/main/LOGO/Gemini_Generated_Image_1ppnm1ppnm1ppnm1%20(1).jfif

Implementation requirements:
- Obtain the actual image asset and place it in the project's public assets.
- Reference the local asset in the application rather than relying on the GitHub preview page.
- Preserve the logo's original proportions and appearance.
- Use the same logo in the header and favicon where technically appropriate.
- Do not generate a replacement logo.

Keep the existing design identity:
- Paper: #F4F1E9
- Charcoal: #242520
- Burnt orange: #B84B2F

Avoid generic AI dashboard styling, purple-blue gradients, excessive rounded cards, unnecessary animations, and symmetrical feature-card layouts.

## 2. Clean up the application header

The current header looks cluttered, particularly around the logo.

Redesign the header into a restrained, professional application navigation.

Desktop:
- Left: logo and DocuLens wordmark, aligned vertically.
- Middle: clear navigation for Library, Search, Compare, and other existing primary destinations.
- Right: only useful actions, such as settings or a clearly labelled help option, if they already exist.
- Use consistent spacing, alignment, typography, and icon sizes.
- Avoid duplicated branding, crowded controls, and unnecessary navigation labels.
- Clearly indicate the active section.

Mobile:
- Show a compact logo and wordmark.
- Use a clean menu or responsive navigation pattern.
- Prevent overlapping, clipped labels, and horizontal overflow.
- Keep the main action easy to reach.

Do not hide important actions or invent nonfunctional buttons. Reuse the existing navigation architecture when possible.

## 3. Upgrade Compare into an intelligent document comparison workspace

The Compare section must support comparing two documents that discuss the same subject, including documents that use different words to describe the same concept.

Examples:
- Two documents explaining computers.
- Two documents explaining data structures.
- Two explanations of algorithms using different terminology.
- Two documents discussing the same technology from different perspectives.
- Two documents whose definitions overlap but are not identical.

### A. Document selection

Provide two clearly labelled selectors:
- Document A — Reference document
- Document B — Document to compare

Allow users to select from existing documents. Show each document's title and useful metadata where available.

Provide a clear swap action to exchange A and B.

Prevent confusing duplicate selection unless comparing a document against itself is intentionally supported.

### B. Comparison modes

Provide a practical comparison mode selector:

1. **Content differences:** identify matching, changed, and document-specific information.
2. **Concept comparison:** find passages discussing the same subject even when they use different wording.
3. **Definition comparison:** compare how both documents define a term, explain a concept, or describe an algorithm.
4. **Topic overlap:** identify subjects present in both documents and subjects found in only one.

Use the existing comparison engine and lexical retrieval as the baseline. Add semantic comparison only where a real implementation is available.

If semantic matching requires an embedding model or remote AI provider, explain the dependency and privacy implications. Do not pretend lexical keyword matching is semantic understanding.

### C. Comparison results

Present the results in a readable workspace with:

- Shared concepts.
- Definitions and explanations from Document A.
- Corresponding explanations from Document B.
- Key similarities.
- Meaningful differences and contradictions.
- Important details found only in Document A.
- Important details found only in Document B.
- Source document, page number, and supporting excerpt for each evidence-backed finding.

For example, if one document describes an algorithm as a step-by-step procedure and another calls it a finite sequence of computational instructions, identify the possible conceptual relationship and show both source passages.

Do not automatically claim that two terms mean exactly the same thing. Label uncertain matches as possible relationships and preserve important distinctions.

### D. Evidence and comparison reliability

- Every substantive comparison finding must be traceable to real extracted document text.
- Keep page numbers accurate.
- Distinguish direct evidence from generated summaries.
- Never invent quotations, definitions, page numbers, or document contents.
- Clearly state when a comparison is inconclusive or evidence is insufficient.
- Do not present a similarity percentage unless it is calculated by a documented, meaningful method.
- If a score is displayed, explain what it measures and its limitations.
- Handle scanned, empty, encrypted, malformed, and partially parsed PDFs gracefully.
- Do not send document content to an external provider without clear disclosure and the appropriate user choice.

### E. Comparison interaction

Allow users to:
- Open a finding in the relevant document.
- Jump to the supporting page.
- View the original passage in context.
- Switch between side-by-side and consolidated results where practical.
- Expand or collapse evidence sections.
- Filter findings by shared information, differences, and unique information.

Keep the workspace focused. Avoid displaying every finding inside a separate oversized card.

## 4. Upgrade search with multiple query colours

Improve document search so that users can search for multiple terms and distinguish each term visually.

Example:
- Search term 1: `computer`
- Search term 2: `algorithm`
- Search term 3: `data`

Give each query term a distinct, accessible highlight colour. Keep the colours consistent between search results, PDF text where highlighting is supported, and the Inspect in Reader experience.

Requirements:
- Highlight all matching occurrences, not just the first match.
- Support case-insensitive matching.
- Support multiple terms at once.
- Clearly distinguish exact phrase matches from individual term matches when practical.
- Do not modify the underlying document text.
- Escape user input safely; never interpret a search query as executable HTML or a regular expression without proper escaping.
- Avoid overlapping highlights obscuring text.
- Ensure highlights remain legible in light and dark or selected states if both are supported.

If the current search only uses extracted text, implement highlighting against the same extracted text and page information. Do not claim to highlight PDF text visually if the PDF viewer does not support that functionality.

## 5. Make “Inspect in Reader” work properly

When a user clicks a search result's **Inspect in Reader** action:

1. Open the correct document.
2. Navigate to the correct page.
3. Scroll to the matching passage where technically possible.
4. Highlight the relevant search terms using the same colour mapping as the search panel.
5. Keep all active search terms available while the user inspects results.
6. Allow moving to the next and previous match.
7. Show the active match count, for example, “Match 3 of 12”.
8. Provide a clear action to remove highlights or clear the current search.

Preserve the user's search context when opening the reader. Make it obvious which result triggered navigation.

Handle cases where the page or text position cannot be located. In those cases, open the correct document and page and explain that precise highlighting is unavailable.

Do not lose highlighting when the user moves between search results if the same query remains active.

## 6. Technical and data requirements

Before implementing:
- Inspect the existing comparison engine, lexical search service, PDF parser, document types, and reader components.
- Reuse existing extracted text and page metadata.
- Add shared utilities for search term matching and highlight ranges instead of duplicating logic.
- Keep PDF parsing and rendering compatible with the existing pdfjs-dist integration.
- Preserve current IndexedDB data and document identifiers.
- Avoid adding a large dependency for functionality that can be implemented safely with existing tools.
- Keep any optional AI integration behind the existing service boundary.
- Never expose API keys in the frontend.

If the code needs a data-model change, explain why and implement a backward-compatible migration where necessary.

## 7. Design quality and accessibility

Make the application feel like a carefully designed document workspace, not a generic AI product.

- Keep typography readable and hierarchy obvious.
- Use the established paper, charcoal, and burnt-orange palette.
- Use distinct but restrained highlight colours for search terms.
- Ensure colour is not the only indicator of meaning; use labels, outlines, or match markers as needed.
- Support keyboard navigation and visible focus.
- Give controls accessible names.
- Ensure responsive layouts work on mobile, tablet, and desktop.
- Provide useful loading, empty, error, and success states.
- Avoid fake data, fake statistics, placeholder actions, and decorative UI that does not help users.

## 8. Testing and delivery

Add or update tests for:
- Comparing two related documents with different terminology.
- Comparing documents with both shared and unique concepts.
- Identifying definitions that are similar but not equivalent.
- Missing or insufficient evidence.
- Invalid citation references and incorrect page numbers.
- Multiple search terms with different highlight colours.
- Special characters and regex-like search input.
- Opening the correct page through Inspect in Reader.
- Next and previous match navigation.
- Empty libraries and deleted documents.
- Responsive navigation and logo asset loading.

Run the available TypeScript checks, linting, tests, and production build. Fix actual failures where possible.

At completion, report:
1. Files changed.
2. Features implemented.
3. Tests actually executed and their results.
4. Features that remain incomplete.
5. Any migration or privacy considerations.

Do not claim that a feature works or that tests passed unless you verified it. Preserve the existing product and deliver incremental, reviewable changes.
--------------------------------------------------------------------
Prompt 1.2
--------------------------------------------------------------------

# DocuLens — Fix Table Extraction, Simplify Header, Improve Reader and Comparison Exports

Act as a senior React + TypeScript engineer specializing in PDF parsing, document intelligence, accessibility, and production-quality UI.

Work on my existing DocuLens repository and inspect the uploaded project before changing anything.

The current issues are:
1. The first two test PDFs contain tables, but DocuLens does not detect them.
2. The global header contains a document selector that takes up space and is confusing outside document-specific workflows.
3. The Reader repeats a “Document:” label that does not add useful information.
4. Compare currently exports a Markdown report, but users also need a well-formatted PDF report.
5. Some UI elements feel cluttered and overly generated instead of deliberately designed.

Make targeted fixes. Do not rewrite the application or replace its architecture.

## 1. Fix actual PDF table extraction

Inspect `src/services/pdfParser.ts`, `src/components/TablesView.tsx`, the document/table types, and the PDF ingestion pipeline.

The first two DocuLens test PDFs contain drawn tables. Investigate why those tables are not detected and fix the actual extraction path.

Important: PDF.js generally extracts positioned text items, not complete semantic table structures. Do not assume that every table is represented as a ready-made HTML-like grid.

Implement a practical extraction pipeline:

### A. Detect table-like page regions
- Use PDF.js text items and their positional metadata.
- Group text items into rows using their vertical positions, with tolerances that account for font size and minor alignment differences.
- Detect likely columns from consistent horizontal positions and gaps between text groups.
- Preserve the reading order and align cells to the appropriate columns.
- Handle multi-line cells, wrapped headings, empty cells, merged-looking cells, and inconsistent spacing where feasible.
- Avoid combining unrelated paragraphs into false tables.

### B. Validate extracted tables
- Require reasonable evidence of a table, such as multiple aligned rows and repeated column positions.
- Avoid treating ordinary prose, bullet lists, or single lines as tables.
- Preserve headers, rows, page numbers, source document IDs, and extraction provenance.
- Report extraction confidence or a clear warning when the structure is uncertain.
- Support more than one table per page.

### C. Provide graceful fallbacks
- If automatic extraction fails, allow users to inspect the page and retry or correct the extracted table where practical.
- Clearly distinguish “no table detected” from “table extraction failed.”
- Never fabricate table cells to fill missing data.
- If a PDF contains scanned images and OCR is unavailable, explain that limitation instead of claiming the page has no tables.

### D. Verify with the existing test PDFs
Use:
- `DocuLens_Test_Document_A_Computers_Algorithms.pdf`
- `DocuLens_Test_Document_B_Computing_Concepts.pdf`
- `DocuLens_Test_Document_C_Search_Tables_Edge_Cases.pdf`

The first two contain synthetic tables. Upload them and verify that the extracted tables preserve the expected rows, columns, and cell values.

Add tests for alignment differences, wrapped text, multiple tables, ordinary paragraphs, and missing table content. Do not hardcode table results based on these particular test filenames.

## 2. Simplify the global header

Inspect `src/components/Header.tsx`.

The header currently contains a global document-scope selector, help button, Settings button with text, online/offline status, navigation, and mobile controls.

Make it cleaner and more compact.

Requirements:
- Keep the DocuLens logo and wordmark on the left.
- Keep the existing Library, Reader, Search, Ask Documents, Tables, and Compare navigation.
- Remove the global document selector from the desktop header and mobile header.
- Remove the separate Help button from the global header if its functionality can be accessed from the Settings or help area without losing important capabilities.
- Keep only a compact Settings gear icon on the right, with an accessible name and tooltip.
- Keep essential online/offline status only if it remains useful and does not crowd the layout.
- Preserve the mobile menu and ensure all navigation remains available.
- Do not remove document selectors from places where they are genuinely needed, such as the Compare workspace or table filtering.

The settings icon must navigate to the existing Settings/Workspace section. Do not create a decorative or nonfunctional button.

Use deliberate spacing and consistent alignment. Avoid a boxed control around every header element. Do not shrink the logo until it becomes unreadable.

## 3. Remove redundant “Document:” text in Reader

Inspect `src/components/ReaderView.tsx` and its parent navigation.

When a document is open, its title should be clear without redundant labels.

Requirements:
- Remove the extra “Document:” prefix if the same information is already visible in the Reader title or toolbar.
- Keep the filename or document title visible in one clear location.
- Keep page navigation, search highlights, notes, and reader actions working.
- Do not remove document selection from the Library or other workflows where it is necessary.
- Ensure changing documents updates the displayed title and page state correctly.
- Do not break navigation from Search, Citations, or Compare into the Reader.

## 4. Add a real PDF export to Compare

Inspect `src/components/CompareView.tsx` and the existing Markdown export.

Keep Markdown export and add a separate **Export PDF** action.

The user should be able to export the current comparison as:
- Markdown (`.md`)
- PDF (`.pdf`)

Both exports must represent the same current comparison mode and relevant comparison results.

### PDF report requirements
Create a clean, professional report with:
- DocuLens branding and report title.
- Reference document title and comparison document title.
- Generation date and selected comparison mode.
- A concise summary of findings.
- Shared concepts.
- Definition comparisons.
- Key differences.
- Topics shared by both documents.
- Topics unique to each document.
- Supporting excerpts, source document names, and page references where available.
- Clear warnings when a result is uncertain or evidence is insufficient.

Formatting:
- Use readable typography, restrained spacing, consistent headings, and page numbers.
- Use the existing paper, charcoal, and burnt-orange visual identity.
- Prevent table rows and long passages from overflowing page boundaries.
- Handle long filenames, quotes, and large comparison reports.
- Use page breaks sensibly and avoid splitting a heading from its following content.
- Do not include empty sections or invent missing findings.
- Do not show similarity scores unless the underlying method is documented and meaningful.

Implementation:
- Prefer an existing reliable PDF export mechanism if the project already has one.
- Otherwise choose the smallest appropriate solution, such as a carefully styled print document or a suitable PDF-generation library.
- If using browser print-to-PDF, provide a clean print stylesheet and an explicit print dialog flow. Do not claim a PDF file was automatically downloaded if the browser only opened a print dialog.
- If using a PDF-generation library, add it through the project's package manager and verify the production build.
- Ensure exports work for long reports, not just a single page.
- Sanitize filenames and clean up temporary resources.

### Markdown export corrections
- Preserve valid Markdown formatting and headings.
- Include the selected comparison mode.
- Escape or format source text safely.
- Include accurate source page references.
- Avoid dumping internal IDs, irrelevant chunk counts, or implementation details into the human-readable report unless they are useful to the reader.
- Keep the output readable when opened in a normal Markdown viewer.

Show clear success or failure feedback for each export.

## 5. Make the interface feel human-designed

Preserve the established DocuLens identity:
- Paper: `#F4F1E9`
- Charcoal: `#242520`
- Burnt orange: `#B84B2F`

Use the existing logo. Do not generate a replacement.

Design rules:
- Prefer clear hierarchy and useful whitespace over decorative cards.
- Keep controls close to the content they affect.
- Avoid unnecessary uppercase labels, excessive borders, repeated rounded containers, fake statistics, and generic AI-style copy.
- Use concise, natural wording.
- Make empty states explain the next useful action.
- Do not animate elements without a clear interaction purpose.
- Ensure the interface works on desktop, tablet, and mobile.
- Preserve keyboard accessibility, visible focus, and readable contrast.

Do not redesign unrelated screens just to make the change look larger.

## 6. Data integrity and compatibility

- Preserve existing IndexedDB documents and IDs.
- Do not delete or reseed the user's library.
- Avoid destructive changes to stored table structures.
- If table extraction changes the schema, add a backward-compatible migration or reprocess option.
- Do not silently overwrite existing extracted tables without a safe recovery path.
- Do not send document contents to external services without disclosure and the required user choice.

## 7. Test and report honestly

Run the available checks:
- TypeScript/lint checks.
- Unit tests.
- Production build.
- PDF extraction tests using all three synthetic PDFs.
- Markdown export tests.
- PDF export tests, including a long report.
- Reader navigation and page-reference regression tests.
- Desktop and mobile header checks.

At completion, provide:
1. Root cause of table extraction failure.
2. Files changed.
3. What was fixed and what remains limited.
4. Actual commands executed and their results.
5. Any added dependencies.
6. Any migration or reprocessing steps required.

Do not claim table detection works unless it has been tested against the PDFs. Do not claim the PDF export works unless an actual exported report has been generated and checked.

Start by inspecting the current implementation, then fix the table extraction issue before polishing the UI.

----------------------------------------------------------------
UI - Color
------------------------------------------------------------------

Redesign the color theme of my React + Tailwind v4 app "DocuLens" (a local-first
document intelligence tool) into a professional dark theme. Change colors only.
Do not change layout, copy, logic, fonts, or component structure.

GOAL
A calm, high-contrast, enterprise-grade dark UI. Neutral blue-grey surfaces,
one restrained amber accent, and muted status colors. It should feel like a
serious research/audit tool, not a flashy app.

PALETTE (use exactly these values)
Page background ........ #0F1217
Card / panel ........... #161B22
Raised / hover / chip .. #1D242E
Border ................. #262D38   (stronger border: #343D4B)
Text primary ........... #E6E9EF
Text secondary ......... #9AA3B2
Text faint ............. #6B7585
Accent (amber) ......... #E8A94A   (hover #D4943A)
Accent subtle bg ....... #2A2112
Accent border .......... #5A4520
Text on accent fill .... #1A1305
Overlay/backdrop ....... black at 60% opacity

CURRENT COLORS TO REPLACE (hardcoded as Tailwind arbitrary values in
src/components/*.tsx, src/App.tsx, index.html, src/index.css)
#F5F2EB -> #0F1217     #FAF8F5 -> #161B22
#ECE7DD / #EAE5D9 / #EAE4D7 / #F4F1E9 -> #1D242E
#E0D9CC -> #262D38     #D5CEBF / #D0C8B8 / #C8BFB0 -> #343D4B
#20211D -> #E6E9EF     #383933 (hover on dark buttons) -> #C5CAD4
#5C5E55 -> #9AA3B2     #8E9085 -> #6B7585
#B84B2F -> #E8A94A     #9F3E25 -> #D4943A
#F9EBE6 -> #2A2112     #E8B4A5 -> #5A4520

RULES
1. Replace colors everywhere they appear. Check text, backgrounds, borders,
   hover and focus states, placeholders, selection color, scrollbars and
   modal overlays.
2. Buttons that used the dark ink background with paper-colored text must keep
   readable contrast on the new theme. Primary buttons are light (#E6E9EF) with
   dark text (#0F1217). Any filled amber element uses dark text (#1A1305).
3. Status colors (red, emerald, amber, rose, blue, stone) must be remapped for
   dark mode. Light tints (the 50-300 stops) become dark translucent tints,
   and dark text (the 700-950 stops) becomes light text. Override them in the
   Tailwind v4 @theme block in src/index.css so the change happens in one place.
   Solid destructive buttons use #C23B3B with white text.
4. Set color-scheme: dark on html, plus <meta name="color-scheme"> and
   <meta name="theme-color" content="#0F1217"> in index.html.
5. Keep WCAG AA contrast (4.5:1 for body text). Check text-secondary on cards,
   amber on dark surfaces, and highlighted search matches.
6. Search highlights and active-tab states use amber at 15-30% opacity with
   amber text. Do not use bright saturated fills.
7. Leave the PDF export (jsPDF) in light colors so printouts stay readable.
8. Where possible, replace repeated hardcoded hex values with the theme tokens
   (bg-paper, bg-paper-light, text-ink, text-ink-muted, border-paper-border,
   text-accent) so the theme can be changed in a single file later.

DELIVERABLE
- List every file changed.
- Confirm that no old light-theme hex values remain (search for the old values
  above).
- Run the build and the tests, and fix anything my changes broke.
- Note any component where contrast looked questionable and how you handled it.
