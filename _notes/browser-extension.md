# Browser Extension Development Plan

### **1. Core Architecture & Sync**

- **Cross-Browser Support:**  
  Build with WebExtension APIs for compatibility with Chrome, Edge, Firefox, and Safari.
- **Authentication & Sync:**  
  - OAuth or token-based authentication to securely connect with the user’s desktop app or cloud backend.
  - Real-time sync status indicator in the extension popup.
- **Desktop App Communication:**  
  - Use WebSocket, local HTTP server, or native messaging for fast, secure communication with the desktop app for content extraction and note storage.

---

### **2. Bookmark Import & Content Extraction**

- **Import Browser Bookmarks:**
  - One-click import of all browser bookmarks.
  - Send URLs to the desktop app, which crawls and extracts full page content (title, text, images, metadata).
  - Progress and error feedback in the extension UI.
- **Batch Operations:**
  - Allow users to select specific bookmark folders or tags for import.
  - Deduplicate URLs before sending.

---

### **3. Contextual Capture (Right-Click Menu)**

- **Save Page/Selection:**
  - Add context menu items:
    - “Save Page to Second Brain”
    - “Save Selection to Second Brain”
  - On click:
    - Capture page URL, title, and either full content or selected text.
    - Optionally prompt for tags, list assignment, or quick note.
    - Send to desktop app for processing and storage.
- **Quick Feedback:**
  - Show a toast/notification on successful save, with a link to open the note in the desktop/mobile app.

---

### **4. Floating Sidebar/Widget**

- **Edge Injection:**
  - Inject a minimal, collapsible floating sidebar on every page (user can disable per site).
  - Sidebar features:
    - **Quick Note:** Instantly create a new note (supports Markdown, screenshots, and attachments).
    - **Global Search:** Search all personal notes/lists/tags with instant results and preview.
    - **Contextual Actions:** Show relevant actions based on the current page (e.g., “Save all videos on this page” for YouTube).
- **Design:**
  - Minimalist, non-intrusive, dark/light mode support.
  - Keyboard shortcut to open/close sidebar.

---

### **5. Smart List Extraction on Supported Sites**

- **Supported Sites:**
  - YouTube (video lists), Bilibili, Xiaohongshu (Rednote), Zhihu (collections), ChatGPT/Claude chat lists, Instagram (saved posts), etc.
- **One-Click Bulk Extraction:**
  - Detect when the user is on a supported list page.
  - Show a prominent “Extract All Links” button in the sidebar or as a floating action button.
  - On click:
    - Parse the DOM for all relevant links/items.
    - Send the list of URLs to the desktop app for batch crawling and content extraction.
    - Optionally, allow user to preview/edit the list before sending.
- **Custom Site Parsers:**
  - Modular parser system for easy addition of new supported sites.
  - Fallback to generic link extraction for unsupported sites.

---

### **6. Advanced Features & UX**

- **Tagging & Organization:**
  - Prompt for tags, list assignment, and quick notes on every capture.
  - Autocomplete tags and lists from the user’s personal knowledge base.
- **AI-Powered Suggestions:**
  - Suggest tags, summaries, or related notes using local or cloud AI models.
- **History & Undo:**
  - View recent captures and undo accidental saves from the extension popup.
- **Settings:**
  - Per-site enable/disable, keyboard shortcuts, appearance, and privacy controls.

---

### **7. Security & Privacy**

- **User Data Protection:**
  - All data is stored locally or in the user’s private cloud/Git repo.
  - No third-party analytics or tracking.
- **Permissions:**
  - Request only the minimum browser permissions required.
  - Transparent permission explanations in the onboarding flow.

---

### **8. Implementation Roadmap**

1. **MVP:**  
   - Popup UI with authentication, right-click save, and sidebar with quick note.
   - Basic communication with desktop app for saving notes.
2. **Bookmark Import & Batch Extraction:**  
   - Full bookmark import and batch link extraction for supported sites.
3. **Sidebar Enhancements:**  
   - Global search, advanced tagging, and AI suggestions.
4. **Custom Site Parsers & Extensibility:**  
   - Modularize site extraction logic for easy updates.
5. **Polish & UX:**  
   - Refine UI, add settings, and optimize performance.

---

### **Example User Flows**

- **Save a Webpage:**  
  Right-click → “Save Page to Second Brain” → (optional) add tags → Success toast.
- **Bulk Save YouTube Playlist:**  
  Open playlist → Sidebar detects YouTube → “Extract All Videos” → Confirm → All video pages sent to desktop for crawling.
- **Quick Note:**  
  Click sidebar → Type note → Save → Instantly synced to personal knowledge base.
