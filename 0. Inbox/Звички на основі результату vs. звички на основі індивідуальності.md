---
tags:
  - zettelkasten
parent: "[[]]"
---
#### 💡 Main Thought  
---
***Замість того щоб фокусуватися лише на результатах, варто будувати звички, що відповідають вашій ідентичності. Це змінює підхід до змін: ви не просто прагнете досягнути результату, ви формуєте особистість, здатну досягати цього результату.***

#### ⚙ Context  
---
**Чимало людей беруться змінювати звички, зосереджуючись на тому, чого їм хочеться досягти. Це приводить нас до звичок, які ґрунтується на результаті. Альтернативою є звички, що ґрунтуються на індивідуальності. У разі такого підходу ми зосереджуємося на тому, ким хочемо стати.**

#### 🔍 Explanation  
---
*Звички, побудовані на основі ідентичності, створюють фундамент для довготривалих змін. Коли людина формує свою самоідентифікацію — наприклад, "я спортсмен" або "я письменник", — це впливає на її поведінку щодня. Відповідно до цього підходу, кожна дія, звичка або рішення повинні відповідати тому, ким ви хочете бути, а не тільки тому, що ви хочете досягти. Таким чином, звички, зосереджені на ідентичності, стають стійкішими і більш ефективними в довгостроковій перспективі.*

#### 🧱 Connections  
---
- [[ ]]  
- [[ ]]


#### 📚 Source / Origin (optional)  
---


#### 🧠 My Commentary (optional)  
---


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