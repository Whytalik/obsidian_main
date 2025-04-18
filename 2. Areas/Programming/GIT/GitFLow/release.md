---
tags:
  - git
parent: "[[Git Flow]]"
---
---

![[Pasted image 20250124125836.png]]

Коли `develop` набере достатньо функцій для випуску (або наближається передбачений термін випуску), ви створюєте гілку `release` від `develop` . Створення цієї гілки запускає наступний цикл випуску, тому після цього моменту не можна додавати нові функції — у цій гілці повинні йти лише виправлення помилок, генерація документації та інші завдання, пов'язані з випуском. Коли він готовий до відправки, гілка `release` зливається з `main` і маркується версією. Крім того, вона повинна бути злитою назад у `develop` , який може змінитися з моменту початку випуску.

Використання окремої гілки для підготовки релізів дозволяє одній команді шліфувати поточний реліз, тоді як інша команда продовжує працювати над функціями для наступного релізу. Це також створює добре визначені фази розробки (наприклад, легко сказати: “Цього тижня ми готуємося до версії 4.0,” і дійсно побачити це в структурі репозиторію). Створення `release` гілок є ще однією простою операцією розгалуження.

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