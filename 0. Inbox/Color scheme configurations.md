---
tags:
  - work
  - general
parent: "[[]]"
---
---
```js
module.exports.schemes = {
  scheme1: {
    color1: '#000000',
    color2: '#ffffff',
    }
};

module.exports.colors = (scheme) => {
  return {
    brandColors: {
      color1: scheme.color1,
      color2: scheme.color2,
      },
  };
};
```

## 🔁 Як усе працює разом?
---
1. Ти **визначаєш різні схеми** в `schemes`.
2. Потім передаєш одну зі схем у функцію `colors(scheme)`.
3. Вона **повертає кольори в потрібному форматі**, який потім може бути використаний у шаблоні, стилях тощо.


Функція `colors` приймає схему і повертає об'єкт з зарезервованих назв і значень для кольору схеми. `colors` може мати наступні зарезервовані назви:
- `blockBackgroundColors` - Налаштування кольорів фону блоку
- `brandColors` - Налаштування типового кольору
- `componentBackgroundColors` - Налаштування кольорів фону компонента
- `containerBackgroundColors` - Налаштування кольорів фону контейнера
- `generalBackgroundColors` - Налаштування кольорів фону вмісту
- `propColors` - Налаштування кольорів властивостей
- `textColors` - Налаштування кольорів тексту

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