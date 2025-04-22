---
tags:
  - work
  - email
parent: "[[]]"
---
---
**Merge теги** — це спеціальні коди, які автоматично підставляють **персональні дані отримувача** у шаблоні листа, щоб зробити email більш **персоналізованим**.

### ✉️ **Що таке merge теги простими словами:**
---
Це як змінні в шаблоні листа. Коли ти надсилаєш email багатьом людям, merge теги підставляють у кожному листі **унікальні дані кожного отримувача**.


### 🧾 **Приклад:**
---
**У шаблоні:**
> Привіт, `{{FirstName}}`!  
> Дякуємо, що ви з нами вже `{{SubscriptionYears}}` років!

**У листі, який отримає Марія:**
> Привіт, Марія!  
> Дякуємо, що ви з нами вже 3 роки!


### 🔄 **Як це працює в eWizard:**
---
- Список доступних merge тегів визначається **цільовою системою** (наприклад, Salesforce, Veeva CRM, Mailchimp).
- Merge теги залежать від:
    - 🔧 **Налаштувань адміністратора** — які змінні дозволено використовувати.
    - 📬 **Системи, у якій буде надісланий лист** — кожна система має свої теги.



```dataviewjs
// Get current note details
const currentFile = dv.current().file;
const currentNote = currentFile.name;

// Get all notes linking to current note (excluding self-references)
const linkingNotes = dv.pages()
    .where(p => 
        (p.file.inlinks.includes(currentNote) || 
        containsLink(p.file.outlinks, currentNote))
    )
    .filter(p => p.file.path !== currentFile.path) // Exclude current note
    .sort(p => p.file.name, "asc");

// Display settings
const MAX_NAME_LENGTH = 50;
const DATE_FORMAT = "MMM dd, yyyy";

// Create styled table with h6 entries
dv.table(
    ["#", "Note", "Location", "Modified"],
    linkingNotes.map((p, index) => {
        const displayName = p.file.name.length > MAX_NAME_LENGTH
            ? p.file.name.substring(0, MAX_NAME_LENGTH) + "..." 
            : p.file.name;
        
        const modifiedDate = p.file.mtime 
            ? p.file.mtime.toFormat(DATE_FORMAT) 
            : "-";

        return [
            `###### ${index + 1}`,
            `###### ${dv.fileLink(p.file.path, false, displayName)}`,
            `###### ${p.file.folder}`,
            `###### ${modifiedDate}`
        ];
    })
);

// Header with h5 styling
if (linkingNotes.length > 0) {
    dv.paragraph(`##### 📌 ${linkingNotes.length} notes reference [[${currentNote}]]`);
} else {
    dv.paragraph(`##### 🔍 No backlinks found for [[${currentNote}]]`);
}

// Helper function to check links
function containsLink(links, targetNote) {
    if (!links) return false;
    return links.some(link => link.path.includes(targetNote));
}

// Minimal styling
dv.el("style", `
    .dataview.table-view-table {
        width: 100%;
        margin: 10px 0;
    }
    .dataview.table-view-table th {
        background-color: var(--background-primary-alt);
        font-weight: 500;
    }
    .dataview.table-view-table td {
        padding: 6px 10px;
        vertical-align: middle;
        font-size: 0.9em;
    }
    h6 {
        margin: 0;
        font-weight: normal;
    }
`);
```