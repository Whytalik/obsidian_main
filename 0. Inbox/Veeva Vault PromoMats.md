---
tags:
  - work
parent: "[[]]"
---
---
**Veeva Vault PromoMats** — це **цифрова система**, яка допомагає компаніям (особливо у фармацевтиці) **створювати, зберігати, перевіряти та поширювати промоматеріали**, при цьому дотримуючись усіх юридичних та регуляторних вимог.

### 🧩 **Що саме робить VVPM:**
---

|Функція|Що означає|
|---|---|
|📂 **Управління контентом**|Створення та зберігання маркетингових матеріалів (PDF, відео, банери тощо)|
|✔️ **Перевірка і затвердження**|Узгодження контенту між медичним, юридичним і регуляторним відділами (MLR)|
|🔄 **Відстеження змін**|Контроль версій, хто що редагував і коли|
|🌍 **Публікація**|Розповсюдження матеріалів у відповідні ринки або системи|
|✅ **Відповідність вимогам**|Забезпечення дотримання стандартів FDA, EMA або локальних регуляцій|

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