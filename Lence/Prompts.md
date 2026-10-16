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
