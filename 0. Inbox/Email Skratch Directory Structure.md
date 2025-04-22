---
tags:
  - work
  - email
parent: "[[]]"
---
---
- `.ewizard/settings.json` - Specifies the project template type, the path configuration for all the directories, plugin settings, and the template repository.
- `build/dev/` - Stores the compiled project source files. This directory appears after you run the `wiz dev` command.
	- `build/dev/app.js` - зберігає скомпільовані джерельні файли проекту. Цей каталог з'являється після виконання команди `wiz dev`.
	- `build/dev/editor.js` - JavaScript-бандл, який використовується в редакторі
	- `build/dev/index.js` - точка входу проекту на JavaScript створена під час збірки для розробки. Цей файл згадується в `index.html`.
	- `build/dev/state.js` - зберігає всі зміни, застосовані до проекту, в редакторі eWizard.
- `common/`
	- `common/blocks/` - зберігає локальні блоки.
	- `common/blocks-library/` - містить блоки, доступні для додавання до проекту в редакторі eWizard.
	- `common/components/` - зберігає локальні файли компонентів Vue.
	- `common/components/components.json` - містить список компонентів, відображених на панелі компонентів редактора eWizard.
	- `common/i18n/localization.json` - містить локалізацію
	- `common/media/` - зберігає загальні медіаресурси — шрифти, зображення, файли PDF, підпис, відео — у спеціально відведених директоріях.
	- `common/styles/main.css`
- `extensions/common.js` - зберігає загальні компоненти проекту, зареєстровані глобально.
- `node_modules/` - встановлені пакети `npm` для проекту. Ви можете встановити залежності проекту, виконавши команду `wiz install`
- `themes/` - зберігає шаблонні теми проекту, які зберігаються в окремих каталогах. Назва каталогу відповідає його темі.
- `.gitignore`
- `App.vue`
- `icon.png`
- `index.html`
- `package.json` - зберігає загальну інформацію про проект та містить список npm-залежностей проекту.
- `package-lock.json` - автоматично створений файл для відстеження версій всіх пакунків, встановлених npm-клієнтом у `node_modules`
- `preview.jpg`
- `readme.md`
- `settings.json` - визначає налаштування проекту залежно від типу шаблону.


#### 🔗 Internal Links  
---
- Related notes:  
  - [[Bundle]]

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