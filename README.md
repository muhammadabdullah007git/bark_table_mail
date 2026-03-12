# Dark Table Mail

A minimalist, high-performance email compose and bulk-mailing client inspired by the `zed.dev` design language. Built for speed, precision, and technical users.

![Design Aesthetic](https://img.shields.io/badge/Design-Zed.dev-blue)
![Backend](https://img.shields.io/badge/Backend-Google%20Apps%20Script-green)
![Theme](https://img.shields.io/badge/Theme-Pure%20Black%20%2F%20Off--white%20%2F%20One%20Dark-black)

## Key Features

### 1. Professional WYSIWYG Editor
- **Office-Suite Experience**: Direct visual editing with zero focus loss when using tools.
- **Advanced Formatting**: 
    - Bold, Italic, Underline, and **Strikethrough**.
    - Text Alignment (**Left, Center, Right**).
    - **Line & Paragraph Spacing**: Adjust vertical rhythm for professional layouts.
    - **Left & Right Indentation**: Fine-tune text positioning.
    - **Expanded Font Sizes**: 7 levels of control from **X-Small** to **Huge**.
    - **Bulleted** and **Numbered** lists.
    - Custom Indentation and Blockquotes.
    - Integrated **Color Picker** for precise text coloring.
- **Source Mode**: Toggle between visual editing and raw HTML source code with seamless synchronization.

### 2. Advanced Bulk Mailing
- **Flexible Data Source**: Click-to-select or drag-and-drop zone for **CSV**, **XLSX**, or **XLS** files.
- **Smart Variable Mapping**: 
    - Automatically detects `{variable}` placeholders in your To, CC, BCC, Subject, and Body.
    - Integrated **How to Use Variables** guide in the help section.
    - Sleek linear mapping interface to link variables to spreadsheet columns.
- **Send Modes**: 
    - **Auto**: Send to the entire list.
    - **Fixed**: Specify an exact number of records to process.
- **Collision Protection**: Precise brace-matching ensures your code/text stays intact unless specifically mapped as a variable.

### 3. Integrated Live Preview
- **Real-time Rendering**: See exactly what your recipient will see, including HTML formatting and layout.
- **Resizable Layout**: Drag the custom resizer handle to adjust the preview width.
- **Metadata Mirroring**: Live preview of Subject and Recipient fields.

### 4. Deep Customization
- **Gear Icon Settings**: Centralized system settings for all application configurations.
- **Dynamic Themes**: 
    - **Pure Black**: OLED-optimized deep black theme.
    - **Off-white**: Professional soft light theme.
    - **One Dark**: Technical blue-gray theme.
    - **GitHub Light**: Clean white developer aesthetic.
- **Dynamic Scaling**: **UI Size** slider that scales fonts, icons, and spacing proportionally across the entire app.
- **UI Font**: Change the primary application font (Inter, Roboto, JetBrains Mono, etc.).

### 5. Modern UX
- **Desktop Feel**: UI elements are unselectable to prevent accidental highlighting, while keeping editors, inputs, and preview content fully interactable.
- **Smart Attachment Zone**: Supports both **drag-and-drop** and **click-to-select** with an adaptive layout.
- **Auto-resetting Inputs**: Intelligent input handling allows you to re-select the same file or color without UI friction.

### 6. Built-in Help System
- **Quick Setup**: The `?` icon provides the exact **Google Apps Script code** and a step-by-step deployment guide.
- **Automated Assistance**: If a GAS URL is missing during send, the app automatically opens the setup guide.

---

## Tech Stack
- **Frontend**: React (TypeScript) + Vite
- **Styling**: Vanilla CSS (Relative `em` scaling & Custom Properties)
- **Parsing**: PapaParse (CSV) & SheetJS (XLSX)
- **Icons**: Custom SVG components
- **Backend**: Any API (Optimized for Google Apps Script)
- **AI-Assisted Development**: Built and maintained with **Gemini CLI** for surgical code updates and rapid feature implementation.

---

## Getting Started

### 1. Installation
```bash
# Clone the repository
git clone <your-repo-url>

# Install dependencies
npm install

# Start development server
npm run dev
```

### 2. Backend Setup (Google Apps Script)
Click the **`?` icon** in the sidebar to copy the backend code, or use this snippet:

```javascript
function doPost(e) {
  try {
    const data = JSON.parse(e.postData.contents);
    MailApp.sendEmail({
      to: data.to.join(','),
      cc: data.cc ? data.cc.join(',') : '',
      bcc: data.bcc ? data.bcc.join(',') : '',
      subject: data.subject,
      htmlBody: data.body,
      attachments: data.attachments ? data.attachments.map(att => {
        return Utilities.newBlob(Utilities.base64Decode(att.data), att.type, att.name);
      }) : []
    });
    return ContentService.createTextOutput("Success").setMimeType(ContentService.MimeType.TEXT);
  } catch (err) {
    return ContentService.createTextOutput("Error: " + err.toString()).setMimeType(ContentService.MimeType.TEXT);
  }
}
```

### 3. Configuration
1. Click the **Gear Icon** in the sidebar.
2. Paste your **Deployment URL** from Google Apps Script.
3. Your settings, including **Theme**, **UI Font**, and **Size**, are saved in cookies.

---

## Security and Privacy
- **Local Processing**: All file parsing and variable replacement happens locally in your browser. No data ever leaves your machine except to your own configured backend.
- **Zero Tracking**: Dark Table Mail does not include any third-party tracking or analytics.

## Deployment

### Deploy to Render
You can easily deploy this project to Render as a static site:

[![Deploy to Render](https://render.com/images/deploy-to-render-button.svg)](https://render.com/deploy?repo=https://github.com/muhammadabdullah007git/dark_table_mail)

1. Connect your GitHub repository to Render.
2. Select **Static Site** as the service type.
3. Use the following settings:
   - **Build Command:** `npm install && npm run build`
   - **Publish Directory:** `dist`

## License
MIT
