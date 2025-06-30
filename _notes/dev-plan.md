# **UI/UX Refactor & AI Integration Plan**

This plan is structured in progressive phases, starting with foundational changes and building towards the more complex, AI-driven features.

**Phase 1: Information Architecture & Core UI Refactor**

This initial phase focuses on updating the app's core terminology and navigation to align with the new vision. It's a crucial first step that creates the foundation for all subsequent features.

1.  **Adopt the "Lists" Metaphor:**
    *   **Objective:** Transition from the "Folders" metaphor to the more encompassing "Lists" concept throughout the application.
    *   **Key Tasks:**
        *   **App Drawer (`lib/widgets/app_drawer.dart`):**
            *   Rename the "Folders" navigation item to "Lists". The corresponding `ListTile` text should be updated to a new localized string (e.g., `context.loc.drawerLists`).
            *   Navigate to a renamed `ListListingScreen`.
        *   **Folder Listing Screen (`lib/folder_listing/view/folder_listing.dart`):**
            *   Rename `FolderListingScreen` to `ListListingScreen` and update its route path.
            *   Modify all user-facing text, such as the `AppBar` title and dialog prompts, from "Folder" to "List" (e.g., "New Standard List", "Rename List").
        *   **Localization:** Update all relevant localization files to reflect this new terminology.

2.  **Refine Main Navigation:**
    *   **Objective:** Reorganize the `AppDrawer` to reflect the new information hierarchy.
    *   **Key Tasks:**
        *   Ensure the primary navigation items in `lib/widgets/app_drawer.dart` are ordered as follows for clarity and priority:
            1.  All Notes
            2.  Lists
            3.  Tags

**Phase 2: Implementing Smart Lists**

This phase introduces the first major intelligent feature, moving beyond simple directory structures.

1.  **Unified List Creation:**
    *   **Objective:** Create a single entry point for creating both standard and smart lists.
    *   **Key Tasks (`ListListingScreen`):**
        *   The Floating Action Button's `onPressed` event will trigger a `showModalBottomSheet`.
        *   This sheet will offer two clear options: "New Standard List" and "New Smart List".
        *   The "Standard List" option will invoke the existing creation dialog (`CreateFolderAlertDialog`, to be renamed).
        *   The "Smart List" option will navigate to a new screen for template selection.

2.  **Smart List Template Gallery:**
    *   **Objective:** Build an intuitive screen for users to discover and create new Smart Lists.
    *   **Key Tasks:**
        *   Develop a new `smart_list_creation_screen.dart`.
        *   This screen will present available templates (e.g., "📥 Todo", "📸 Screenshots", "📚 Readwise") using `Card` widgets with icons and concise descriptions.
        *   A new mechanism (e.g., a JSON config file in the git repo) will be needed to store the definitions of active Smart Lists.

3.  **Integrated List Display:**
    *   **Objective:** Display both standard and smart lists seamlessly in the `ListListingScreen`.
    *   **Key Tasks:**
        *   Update the `ListListingScreen` to source its items from two places: the file system (for standard lists) and the new configuration file (for smart lists).
        *   Visually differentiate Smart Lists from Standard Lists. Using a distinct icon (e.g., a sparkle ✨ or lightning bolt ⚡️) next to the name will provide an immediate visual cue.

4.  **"Todo" Smart List Implementation:**
    *   **Objective:** Implement the logic for the first Smart List.
    *   **Key Tasks:**
        *   Create a new `NotesFolder` subclass (e.g., `TodoNotesFolder`).
        *   This class will be responsible for scanning all notes, parsing for unchecked Markdown tasks (`[ ] ...`), and presenting each task as a virtual item.
        *   The view for this list will need a custom item renderer that displays the task content and a reference to the source note. Tapping an item should navigate the user directly to that line in the note editor.

**Phase 3: AI Chat Interface**

This phase focuses on crafting the centerpiece AI feature: a conversational interface to the user's knowledge base.

1.  **AI Chat Entry Point:**
    *   **Objective:** Provide a prominent and intuitive access point to the chat feature.
    *   **Key Tasks:**
        *   Introduce a new, persistent navigation element. A Floating Action Button with a chat icon on the primary `HomeScreen` or a dedicated tab in a new bottom navigation bar would be ideal.
        *   This button will navigate to the `ai_chat_screen.dart`.

2.  **Chat UI Construction:**
    *   **Objective:** Design and build a clean, familiar, and responsive chat interface.
    *   **Key Tasks (`ai_chat_screen.dart`):**
        *   The layout will consist of a scrollable message history and a text input field pinned to the bottom.
        *   The message history will be built with a `ListView` or `CustomScrollView`, efficiently handling long conversations.
        *   User and AI messages will be styled in distinct chat bubbles.

3.  **Trust-Building UX: AI Responses with Citations:**
    *   **Objective:** Implement the "Source Cards" UI, a critical feature for ensuring transparency and building user trust in the AI's responses.
    *   **Key Tasks:**
        *   The data model for an AI message must include both the generated text and a list of source note identifiers.
        *   An AI message bubble will be a composite widget containing:
            1.  **Source Carousel:** A horizontally-scrolling `ListView` of `Card` widgets displayed *above* the AI's text response. Each card represents a source note, showing its title and a relevant snippet.
            2.  **Actionable Cards:** Tapping a Source Card will navigate the user directly to that note, allowing for immediate context verification.
            3.  **AI Message:** The AI's response, rendered below the source cards with full Markdown support.

**Phase 4: Editor & Reminder Enhancements**

This final phase refines the note-taking experience with integrated actions and reminders.

1.  **Inline Task Reminders:**
    *   **Objective:** Allow users to attach reminders directly to todo items within a note.
    *   **Key Tasks (`NoteEditor`):**
        *   Dynamically render a bell icon (🛎️) adjacent to any line containing a Markdown todo (`[ ]`).
        *   On tapping the bell, present a native date and time picker.
        *   Store the reminder metadata in a clean, non-standard format within the line itself (e.g., `[ ] Buy milk {due: 2024-07-21T10:00:00}`).
        *   The editor's rendering logic will parse this metadata to visually update the bell icon (e.g., filling it with color) when a reminder is set, while keeping the metadata string itself hidden from view.
