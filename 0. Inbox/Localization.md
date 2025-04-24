---
tags:
  - work
  - general
parent: "[[]]"
---
---
```json
// ./settings.json

"localization": {
  "current": "eng",
  "original": "ukr",
  "langs": [
    "eng",
    "fra",
    "ukr"
  ],
  "country": "United Kingdom",
  "fallbacks": [
    "ukr",
    "fra"
  ]
}
```

У файлі `./settings.json` ви можете налаштувати `localization` для інших мов.
1. Встановіть мови `current` і `original` .
    - `current` є цільовою мовою, на яку ви перекладаєте. Після перекладу текст вашого елемента відображається в цій мові. Ви вибираєте мову `current` , коли створюєте свій елемент у платформі eWizard. Код мови повинен мати трилітерний ISO 3 формат (наприклад, `eng` , `deu` або `ukr` ).
    - `original` є мовою джерела, з якої ви перекладаєте. Мова `original` є мовою `current` попередньої версії вашого елемента. Англійська є базовою оригінальною мовою в платформі eWizard.

2. Додайте мови локалізації до `langs` масиву, щоб відображати текст вашого елемента в цій мові, коли ви обираєте її в платформі eWizard.
	- `langs` є списком мов локалізації, які ви додали для вашого елемента в платформі eWizard. Коли ви обираєте мову з наявною локалізацією в платформі eWizard, ваш елемент відображається в цій мові.

3. Додайте мови до `fallbacks` .
    - `fallbacks` є списком вибраних як `current` мов відновлення в платформі eWizard у попередніх версіях елемента. Мови відновлення використовуються для локалізації, якщо для `current` мови немає локалізації. eWizard.js використовує `original` мову як основну мову відновлення, якщо для `current` мови немає локалізації. Якщо якийсь текст не локалізовано для `current` або `original` мови, eWizard.js використовує наступну мову відновлення з списку.
4. Встановіть країну локалізації в `country` . Це поле не впливає на локалізацію.

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