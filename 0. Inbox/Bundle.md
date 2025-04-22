---
tags:
  - programing
  - work
parent: "[[]]"
---
---
**Бандл (bundle)** — це **згрупований файл**, який містить **весь JavaScript-код, необхідний для роботи програми** (у цьому випадку — редактора).

📦 Уяви, що у тебе є багато окремих JS-файлів (наприклад, кнопки, логіка, меню, інтерфейс).  
Щоб браузер не завантажував кожен файл окремо, **усі файли об’єднують в один або кілька "бандлів"**.


### 🧠 Простими словами:
---
> JavaScript-бандл — це як "один великий файл", у який зібрано весь код для того, щоб програма працювала швидко і правильно.

### 🛠️ Навіщо потрібен бандл?
---

|Перевага|Пояснення|
|---|---|
|🚀 Швидше завантаження|Менше HTTP-запитів → швидша робота в браузері|
|🧹 Менше помилок і конфліктів|Усе зібрано централізовано, з урахуванням залежностей|
|🔐 Оптимізація і захист коду|Код можна стиснути (minify), приховати структуру (обфускація)|

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