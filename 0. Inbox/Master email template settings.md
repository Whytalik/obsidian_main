---
tags:
  - work
  - email
parent: "[[Settings]]"
---
---
Можна створити шаблон email для певної марки, мови, країни та цільової системи. Для цього додайте відповідні поля до файлу `settings.json` та встановіть необхідні значення.
```json
{
  "name": "Viseven Default eMail",
  "id": "41bddf687d7b3691a68f180bd999ddc3",
  "metadata": {
    "purpose": {
        "default": "invitation",
        "current": "follow-up"
    }
  },
  "localization": {
    "current": "deu",
    "original": "eng",
    "langs": ["eng"],
    "country": "Germany"
  },
  "browserslist": ["last 2 versions"],
  "screenshoter": {
    "asImageInPdf": true,
    "delay": 1000,
    "icons": {
      "blocks": {
        "enabled": true,
        "width": "200px",
        "mode": "view"
      }
    }
  },
  "app": "./App.vue",
  "targetCLM": {
    "name": "Veeva Vault",
    "code": "veeva"
  },
  "theme": "Viseven",
  "templateType": "Broadcast",
  "templateSubType": "SFMC",
  "assetsGroup": {
    "blocks": "Viseven",
    "components": "broadcast"
  },
  "writeFrameworkVersion": false,
  "content": {
    "automaticLink": false
  },
  "fonts": {
    "alternative": "Helvetica, sans-serif",
    "external": [
      "Arial",
      {
        "name": "Custom Font",
        "fontFamily": "Noto Sans",
        "alternative": ""
      }
    ]
  },
  "optimization": {
    "maxImageWidth": 640,
    "minifyClassesFilter": [
      "block",
      "break-columns",
      "button-container",
      "button-text",
      "wiz-title",
      "root"
    ]
  },
  "uncss": {
    "ignore": [
      "/\\.block/",
      "/\\.break-columns/",
      "/\\.button-container/",
      "/\\.root/"
    ]
  },
  "information": {
    "brand": "5e78d93f5555f900088d5990"
  },
  "externalSystems": {
    "contentful": {
      "twoWaySync": true
    }
  }
}
```

- `purpose` - мета email. Вона визначає відображення стандартних блоків у шаблоні електронної пошти. `default` є стандартною метою email, яка відображається спочатку у списку. `current` є поточною метою, застосованою до шаблону електронної пошти.
- `localization.country` - інформація про мови та локалізації шаблону email. У цьому шаблоні німецька ( `deu` ) встановлена як `current` мова, а англійська ( `eng` ) — стандартна мова будь-якого шаблону email — зберігається як `original` . Поле `langs` містить одну доступну `eng` локалізацію для цього шаблону.
- `browserslist` - налаштування сумісності шаблону електронної пошти з версіями email клієнтів.
- `screenshoter.asImageInPdf` - встановіть значення `true` , щоб експортувати блоки як зображення в PDF. Типовим значенням є `true`.
- `localization` - інформація про країну шаблону електронної пошти. Звідси значення встановлено на `Germany`.
- `screenshoter.delay` - затримка, з якою генерується іконка в мілісекундах.
- `screenshoter.icons.blocks.enabled` - булева властивість, яка визначає, чи включено автоматичну генерацію іконок блоків. Типовим значенням є `false`.
- `screenshoter.icons.blocks.width` - визначає ширину створених іконок блоків у пікселях. Властивість працює, якщо `screenshoter.icons.blocks.enabled` дорівнює `true` .
- `screenshoter.icons.blocks.mode` - визначає, чи генеруються іконки блоків у режимі **PREVIEW** або **EDIT** редактора. Стандартне значення — `view` . Властивість працює, якщо `screenshoter.icons.blocks.enabled` є `true`.
- `app` - шлях до `App.vue` — кореневий файл, який визначає шаблон створеного email. `App.vue` містить додані блоки з вмістом та стилями електронного листа, імпортованими до шаблону.
- `targetCLM` - інформація про цільову систему шаблону електронного листа. У цьому прикладі, це встановлено на `veeva` . Результатний електронний лист сумісний з Veeva Vault.
- `theme` - інформація про поточну тему. Конфігурації тем зберігаються в директорії `themes` кореневої директорії проекту.
- `templateType` - застаріле поле, що вказувало тип шаблону email. Значення `type` вказане у файлі `./.ewizard/settings.json` .
- `templateSubType` - застаріле поле, що вказувало цільову систему шаблону електронної пошти. Значення `subtype` вказане у файлі `./.ewizard/settings.json` .
- `assetsGroup` - інформація про налаштування блоків, компонентів та модулів у каталозі `./assets` . Цей каталог доступний у старих шаблонах електронної пошти. Для нових шаблонів електронної пошти з динамічними темами, файли налаштувань блоків та модулів зберігаються у каталозі `./common/blocks-library` .
- `optimization` - перелік класів, створений вручну, з назвами, які повинні залишатися незмінними після *email build optimization*. Перелік класів можна оновити за допомогою eWizard.js під час експорту Veeva Vault build.
- `maxImageWidth` - визначте ширину зображення в пікселях для зменшення його розміру в результаті створення email. За замовчуванням, eWizard.js зменшує ширину зображення до 1400 пікселів.
- `uncss` - cписок класів, які необхідні для Veeva Vault build. Для додаткової інформації дивіться оптимізація створення електронної пошти Veeva Vault.
- `information` - інформація про бренд шаблону email.
- `writeFrameworkVersion` - встановіть значення `true`, щоб додати версію фреймворку до результатного HTML-файлу при експорті email за допомогою платформи eWizard. Типовим значенням є `true` .
- `automaticLink` - встановіть значення `true` , щоб зробити всі числа клікабельними в результатному HTML після експорту email за допомогою платформи eWizard. Типовим значенням є `false` . У цьому випадку eWizard.js застосовує виправлення, щоб числа не перетворювалися на клікабельні посилання.
- `fonts` - налаштування для налаштування власних шрифтів, які доступні в текстових властивостях редактора eWizard. Використовуйте поле `external` для додавання ваших власних шрифтів `name` та `fontFamily` .
- `externalSystems.contentful.twoWaySync` - встановіть на `true` для активації синхронізації з Contentful для електронної пошти. Якщо до шаблону додані атрибути `data-asset-id` , email створюється в Contentful, коли ви додаєте email в бібліотеку eWizard або завантажуєте архів. Якщо шаблон не містить атрибутів `data-asset-id` , вміст синхронізується з Contentful, коли ви редагуєте завантажений шаблон у редакторі та зберігаєте зміни.

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