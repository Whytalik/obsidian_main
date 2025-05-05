---
tags:
  - work
  - email
parent: "[[Dynamic template]]"
---
---
Ви можете налаштувати відображення блоків для певних країн і мов на вкладці "Блоки" в редакторі eWizard. Коли ви вибираєте елемент країна та мова в бібліотеці eWizard, блоки фільтруються та відображаються відповідно до ваших налаштувань.

Введіть `countries` та `languages` у файл `blocks-themes.json` , щоб відфільтрувати блоки.

У eWizard.js 5.34.0 та пізніших версіях, якщо `countries` та `languages` є об'єктами в обох `blocks.json` та `blocks-themes.json` , eWizard визнає значення з поля з найвищим пріоритетом для відображення блоків на розмітці редактора та в бічній панелі редактора.

Порядок пріоритетності розташування від найвищого до найнижчого:
1. Поле defaultBlocks у `blocks-themes.json` .
2. Поле `blocks` у файлі `blocks-themes.json` .
3. The `blocks.json` file.  Файл `blocks.json`

Пріоритет бічної панелі від найвищого до найнижчого:
1. Поле `blocks` у файлі `blocks-themes.json` .
2. The `blocks.json` file.  Файл `blocks.json` .

Об'єкт `countries` має дві масиви:
- Таблиця `include` містить країни, для яких відображається блок. Наприклад, `block-1` відображається лише для `Ukraine` , `Britain` та `Sweden`.

```json
// ./common/blocks-library/blocks-themes.json

{
  "themes": {
    "Unbranded": {
      "defaultBlocks": [
        {
          "id": "block-1",
          "countries": {
            "include": ["Ukraine", "Britain", "Sweden"],
            "exclude": ["Germany", "France"]
          },
          "languages": []
        }
      ]
    }
  }
}

```

Для відображення блока для всіх країн залиште масив `include` порожнім, введіть `true` або `Global` . Наприклад, `block-1` і `block-2` відображаються для всіх цілей:

```json
// ./common/blocks-library/blocks-themes.json

"defaultBlocks": [
  {
    "id": "block-1",
    "countries": {
      "include": [],
      "exclude": false
    }
  },
  {
    "id": "block-2",
    "countries": {
      "include": true,
      "exclude": []
    }
  }
]

```

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