**1. Overview**

We aim to evolve the app from a powerful, developer-centric note-taking tool into a more versatile "second brain" for a broader audience. The core of GitJournal—markdown-first, Git-synced notes—will be preserved and enhanced with intelligent organization, reminders, and AI-powered knowledge discovery.

**2. Core Design Principles**

*   **Frictionless Capture**: Make it effortless to get information into GitJournal, whether it's a typed thought, a screenshot, or a web highlight.
*   **Intelligent Organization**: Move beyond manual folder management with automated, rule-based organization (Smart Lists).
*   **Connected Knowledge**: Foster connections between ideas through robust tagging and bi-directional linking.
*   **Conversational Discovery**: Enable users to interact with their knowledge base through a natural language chat interface.
*   **Aesthetic Refinement**: Maintain the clean, minimalist aesthetic while introducing new features. UI elements should be intuitive, and microinteractions should provide delightful and meaningful feedback.

**3. Feature Specifications**

**3.1. Information Architecture: The "Lists" Metaphor**

To better reflect the new organizational capabilities, "Folders" will be renamed to **"Lists"** throughout the application. The sidebar navigation will be updated accordingly:

*   All Notes
*   Lists
*   Tags

This change sets the stage for a more flexible system that encompasses both user-managed directories (Standard Lists) and automated collections (Smart Lists).

**3.2. Smart Lists: Your Automated Organizers**

Smart Lists are virtual collections of notes that update automatically based on a set of rules.

**UI Flow:**
1.  A "+" button on the "Lists" screen will present two options: "New Standard List" and "New Smart List".
2.  Selecting "New Smart List" will offer a choice of pre-configured templates.

**Smart List Templates:**

*   **📥 Todo:**
    *   **Functionality:** Aggregates all unchecked markdown todo items (`[ ] ...`) from all notes into a single, dynamic view.
    *   **UI:** Each item in the list will display the task text and the name of the source note. Tapping an item navigates directly to that line in the source note for context. Checking an item here will mark it as done (`[x] ...`) in the source file.

*   **📸 Screenshots:**
    *   **Functionality:** The app will request permission to monitor the device's screenshot directory. New screenshots will be processed in the background.
    *   **OCR & AI:** We will use Google Vision API to:
        1.  Extract all text from the image.
        2.  For images with minimal text, generate a descriptive summary of the image content (e.g., "A chart showing website traffic growth").
    *   **UI:** A new note is created in a dedicated `_screenshots` folder (hidden from standard lists). The note will contain the extracted text/description, with the original screenshot embedded. The "Screenshots" Smart List displays all notes from this folder.

*   **📚 Readwise:**
    *   **Functionality:** Integrates with the Readwise API. Users can connect their account in Settings.
    *   **Sync:** The app will periodically fetch new highlights from articles, books, and tweets. Each source (e.g., a book) will become a new note, and the content will be the user's highlights.
    *   **UI:** The "Readwise" Smart List will display all notes imported from Readwise.

**3.3. Reminders: Never Miss a Thing**

**Note-Level Reminders:**
*   **UI:** In the note editor, the "more" menu (`...`) will include an "Add Reminder" option.
*   **Interaction:** Tapping this opens a native date and time picker. Once set, a small clock icon with the due date appears in the note's header area.

**Todo Item Reminders:**
*   **UI:** When a line contains a markdown todo item (`[ ]`), a small bell icon **(🛎️)** will appear to the right of the line upon hover or tap.
*   **Interaction:** Tapping the bell icon opens a compact date/time picker. Once set, the bell icon becomes filled, and the due time is subtly displayed next to the task. This would be stored as a non-standard markdown extension, e.g., `[ ] Buy milk {due: 2024-07-21T10:00:00}` but rendered in a user-friendly way.
*   **UX Microinteraction:** A gentle pulse animation on the bell icon when a task is due today could draw attention without being intrusive.

**3.4. Organization: Tags & Note Linking**

*   **Tags:**
    *   **Functionality:** Users can add tags anywhere in a note using the `#tagname` or `#tag/with/hierarchy` syntax.
    *   **UI:** Tags will be automatically parsed and styled distinctly. The "Tags" section in the main navigation will display all unique tags in a list or cloud, allowing users to filter notes by tag.

*   **Note Linking:**
    *   **Functionality:** Create links between notes using `[[Note Title]]` wiki-link syntax.
    *   **UI:** The app will support autocomplete when a user types `[[`. When a link is created, it's rendered as a tappable element.

**3.5. AI Chat: Converse with Your Knowledge**

A new, dedicated chat interface allows users to ask questions and get answers sourced from their own notes.

**UI Flow:**
1.  A primary navigation entry point (e.g., a chat bubble icon in a bottom tab bar or a Floating Action Button) will open the AI Chat view.
2.  The interface will be a familiar chat layout: a scrollable history of messages and an input field at the bottom.

**AI Response with Citations:**
*   **Functionality:** When a user asks a question, the backend AI searches the user's notes for relevant information. The generated answer is synthesized from the content of these source notes.
*   **UI:** Crucially, each AI response will be preceded by its sources.
    *   **Source Cards:** Above the AI's message bubble, a horizontally scrolling carousel of "Source Note" cards will be displayed.
    *   Each card will show the note's title and a relevant snippet.
    *   Tapping a source card will navigate the user to that specific note, allowing them to verify the information and explore the original context. This transparency is key to building trust in the AI feature.

**Example Chat Interaction:**
> **[USER]**
> What were my key takeaways from the "Atomic Habits" book?
>
> **[AI]**
>
> *[Card: "Atomic Habits - Highlights"]* *[Card: "Meeting Notes 2024-05-10"]*
>
> You highlighted that creating an "identity-based habit" is more effective than focusing on goals. You also noted that habit stacking—linking a new habit to an existing one—is a powerful strategy. In your meeting notes, you mentioned applying this by adding a 5-minute journal entry after your morning coffee.

**4. Interoperability and Future Vision**

This section outlines forward-looking ideas that build on the core functionalities of GitJournal, enhancing its position as a central hub for personal knowledge management.

*   **Obsidian & Logseq Vault Compatibility:**
    *   **Concept:** Since GitJournal syncs notes via Git, we can extend it to directly open and use an existing [Obsidian](https://obsidian.md/) or [Logseq](https://logseq.com/) vault. Users could point the app to a local folder or a Git repository containing their vault.
    *   **Benefit:** This creates a seamless, interoperable ecosystem. Users can leverage the unique strengths of GitJournal (mobile-first capture, AI chat) alongside the powerful desktop-oriented features of Obsidian/Logseq, all on the same set of markdown files. It respects the user's data and avoids lock-in.

*   **Backlinks (Linked Mentions):**
    *   **Concept:** In a note's info panel, we will display a "Linked Mentions" section.
    *   **Benefit:** This will show all other notes that link *to* the current one, creating true bi-directional linking and helping users discover hidden connections between their ideas. 