---
tags:
  - work
parent: "[[]]"
---
---
**MLR Acceleration** — це **AI-інструмент**, який допомагає **швидше проходити перевірку** медичних, юридичних і регуляторних відділів (**Medical, Legal, Regulatory — MLR**) перед запуском промоматеріалів.

🔹 Його мета — **зменшити час затвердження** та **автоматизувати рутинні перевірки**, при цьому залишаючись у рамках регуляторних вимог.

---

### 🤖 **Як це працює?**
---
Цей інструмент використовує **штучний інтелект та машинне навчання**, щоб:
1. **Аналізувати вміст** твого матеріалу — як **текст**, так і **зображення**.
2. Перевіряти зв’язані **твердження (claims)**, **повторно використовувані тексти**, **модулі**.
3. Визначати **ризики для затвердження** й **оцінювати ймовірність проходження MLR**.

### ✅ **Що ти отримуєш завдяки MLR Acceleration:**
---

|Перевага|Пояснення|
|---|---|
|🔍 **Автоматичний аналіз контенту**|Система сама вказує на потенційні проблеми в контенті|
|📊 **Оцінка ризику MLR**|Ти бачиш оцінку ризику — наскільки вірогідно, що контент пройде MLR|
|🌍 **Перевірка згідно з ринком**|Враховуються специфічні регуляторні вимоги різних країн|



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