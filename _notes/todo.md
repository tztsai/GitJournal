## Quick Fixes

- [ ] Add description field in a checklist editor
  - [ ] When a note is converted to a checklist, the original note is shown in the description field
- [ ] Simplify Views
  - [x] Merge "card" view and "grid" view, c.f. Keep Notes
  - [ ] Group notes on the same day in "journal" view, show time in headers
  - [ ] Rename "standard" view to "list"
  - [ ] Convert the modal to a dropdown menu
- [ ] Fix the UI bugs in "Customize View" (not reactive)
- [ ] Remove the "View Options" - only display titles if exist (c.f. Keep Notes)
- [ ] Unify file naming - `yyyy-mm-dd-hh-mm-ss.md`
  - [ ] For auto-imported files, their names may collide, so add `_TITLE` as prefix
- [ ] Always start with the view mode when opening an existing note, the edit mode when creating a new note
  - [ ] Double tap to enter the edit mode if in the view mode
- [ ] Change the "Choose Editor" modal to dropdown menu
  - [ ] Remove "Journal Editor". Now options are:
        Markdown, Raw, Checklist
- [ ] Change the "Edit File Name" option in the "..." menu in an editor to "Properties"
  - [ ] Timestamp (auto updates the filename if it's not specified)
  - [ ] File Name
  - [ ] Tags
  - [ ] Lists (Favorite, Archive, etc.)
  - [ ] References
  - [ ] Reminders
- [ ] Replace the "..." menu at top right with "Sorting Options"
- [ ] Fix the preview of notes with images or checklists (c.f. Keep Notes)
  - [ ] Display image thumbnails
  - [ ] Display checkboxes
- [ ] Change the logic of note attachments (should be in YAML metadata instead of saving their URIs in the note body)
- [ ] Rename "Root Folder" to "Inbox"
- [ ] Remove the Pro requirement for tags

## New Features

- [ ] Add more options to create special notes in the bottom bar
  - [ ] Image note (image as attachment)
  - [ ] Voice note (audio as attachment)
  - [ ] URL note (webpage content as note)
  - [ ] Chat note (starts an AI chat which will be saved as a note)
  - [ ] Remove the MD and Journal options. Now options are:
        Image, Voice, Checklist, URL, Chat
- [ ] User can select folders for scheduled scans to auto-import files as notes
  - [ ] MD/TXT files -> notes with the file content
  - [ ] Image files -> empty notes with image attachments
  - [ ] Audio files -> empty notes with audio attachments, displayed in waveform UI with play/pause buttons and draggable progress bar
  - [ ] (future) PDF files -> notes with both text and images
  - [ ] Each scanned folder is mapped to a List in the app
- [ ] User can set up service workers to auto-import content from the web
  - [ ] Readwise, via API
  - [ ] Weread, via API (needs manual login to get cookies)
  - [ ] (future) Public YouTube/Bilibili video lists (via API)
  - [ ] (future) RSS feeds, Email newsletters
- [ ] Auto or manual text extraction from media files
  - [ ] Image: Tesseract (free) or Gemini (paid; write a prompt to generate result including both recognized text and description of the image)
    - [ ] Special types: math formula -> LaTeX, table -> MD table, diagram -> Mermaid
  - [ ] Audio: Google Cloud Speech-to-Text API (paid)
    - [ ] (future) With timestamps. Pressing a segment in the view mode will jump to the corresponding time in the audio file.
  - [ ] Video: simply extract the audio track and process it as audio
- [ ] Upgrade the search bar
  - [ ] Limit the number of search results
  - [ ] Show a "More" indicator when there are more results (initial search results should be limited to such a number that "More" should be visible without scrolling down)
  - [ ] Allow user to swipe up or press "More" to load more results
  - [ ] At the end of search results, add an "Ask AI" button to get a Perplexity-style answer (with citations of notes in the repo)
- [ ] Add a welcoming TODO note for new users
- [ ] Note template: a new note can also be created from a template from clicking a Ruminer URI with fields as query parameters
- [ ] Show git history of a note
- [ ] Build a "Swipe" view to continuously swipe through notes
  - [ ] Swipe left or right to like or dislike a note
  - [ ] Scroll down a long note
  - [ ] Drag down to show the search bar (filter the range of notes for swiping)
- [ ] Make the app interoperable with Obsidian and Logseq on the same Git repository
- [ ] Add expand/collapse toggles at the left of each section title (in both view and edit modes)
- [ ] Develop REST API for this app
  - Create a note
    - Create a note from URL (webpage, image, audio, video) (a job is created to fetch the content)
  - Search notes (design the search query language)
  - Get a note
- [ ] (future) Build an MCP server based on the API

## Browser Extension

- [ ] Save the current webpage or selected text as a note
- [ ] Bulk import from a list of URLs on the current page
