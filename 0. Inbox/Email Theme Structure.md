---
tags:
  - work
  - email
parent: "[[Dynamic template]]"
---
---
Тема в шаблоні електронної пошти eWizard.js складається з:
- Файлу `./common/styles/theme.scss` з CSS стилями для кольорових схем марки тощо.
- Директорія `./themes/` , яка містить піддиректорії тем бренду з файлами CSS, медіаресурсами та файлом `index.js` з списком змінних, які доступні в шаблоні під ключем `$theme` .
- Файл `./themes/themes.json` , який містить налаштування для вибору тем у вікні створення нового об'єкта eWizard. Файл містить список доступних тем.

**Структура** має наступний вигляд.
```
.
├─themes/
|  ├─theme1/
|  |  ├─media/
|  |  |  └─images/
|  |  ├─index.js
|  |  ├─index.scss
|  |  └─variables.scss
|  ├─theme2/
|  └─themes.json
```

Де
- `themes` є каталогом, який містить підкаталоги з конкретними темами.
- `theme1` , `theme2` , тощо є підкаталогом теми. 
- `media` є підкаталогом, що містить медіаресурси. Наприклад, зображення.
- `index.js` є списком змінних, доступних у шаблоні під ключем `$ theme`. 
- `variables.scss` є списком Sass змінних, які ви використовуєте в темі.
- `index.scss` є точкою входу для теми. Цей файл містить імпорти.

#### 🔗 Internal Links  
---
- Related notes:  
  - [[themes.json]]
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