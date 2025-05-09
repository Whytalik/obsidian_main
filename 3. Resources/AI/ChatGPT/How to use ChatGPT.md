---
tags:
  - knowledge
  - ai
parent: "[[]]"
---
---
Ось таблиця з усіма варіантами використання ChatGPT, зібраними з наданих фрагментів:

| №   | Принцип запиту                 | Формулювання запиту (що писати в ChatGPT)                                                                                                                                                                                                                                                    |
| --- | ------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | Оптимізація продуктивності     | "Розроби для мене індивідуальну систему підвищення продуктивності, що ґрунтується на моєму звичайному робочому дні, включно з методами управління своїм часом, визначенням пріоритетів завдань і зменшенням факторів, які відволікають, під час роботи над [конкретною метою або проектом]." |
| 2   | Індивідуальний план навчання   | "Створи детальний план навчання, щоб я міг стати експертом у [конкретному предметі або навичці] в [бажані терміни]. Включи щоденний розклад занять, рекомендовані ресурси та контрольні точки."                                                                                              |
| 3   | План розвитку навичок          | "Склади для мене пошвидку практики нових розвитку і першу?" (або варіант: "Склади для мене покрокову дорожню карту розвитку [певної навички чи хобі]. Включи до неї етапи від початкового до просунутого рівня та практичні вправи.")                                                        |
| 4   | Покращення критичного мислення | "Надай мені список складних уявних експериментів і філософських запитань, що стосуються [певної теми або галузі], які допоможуть поліпшити мої навички критичного мислення."                                                                                                                 |
| 5   | План особистого розвитку       | "Розроби для мене особистий план розвитку, спрямований на підвищення мого емоційного інтелекту та навичок міжособистісного спілкування, особливо в [конкретному контексті або оточенні]. Включи до нього заходи та вправи на роздуми."                                                       |
| 6   | Глибоке занурення в тему       | "Стань моїм персональним експертом по [темі]: Розкажи про ключові концепції, поділись реальними прикладами з життя і склади для мене план освоєння теми на місяць вперед."                                                                                                                   |
| 7   | Персональний коуч              | "Потрібна твоя порада! Допоможи скласти індивідуальну програму навчання [темі]. Розпиши щоденні завдання, порадь корисні матеріали та практичні вправи для прокачки навичок."                                                                                                                |
| 8   | Розвиток критичного мислення   | "Давай пограємо! Задай мені серію питань по [темі], прокоментуй мої відповіді і підкажи, як покращити моє критичне мислення."                                                                                                                                                                |
| 9   | Метод Сократа                  | "Проведи зі мною сократичний діалог про [концепцію]. Задавай навідні питання, які допоможуть мені дістатися до суті і покроково покращити розуміння теми."                                                                                                                                   |
| 10  | Історичний контекст            | "Розкажи детально, як [історична подія] вплинула на [сферу]. Проведи паралелі з сучасністю і поділись важливими уроками з минулого."                                                                                                                                                         |
| 11  | Особистий наставник            | "Побудуй моїм ментором в [темі]: Поділись інсайдами, лайфхаками і попереди про типові помилки новачків. Як їх уникнути?"                                                                                                                                                                     |



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