---
tags:
  - work
  - email
parent: "[[]]"
---
---
```json
{
    "content": {
        "type": "email",
        "subtype": "layout"
    },
    "screenshoter": {
        "slideWithCommonLayout": ""
    },
    "path": {
        "blocks": "node_modules/@blocks",
        "blocksFilename": "blocks.json",
        "blocksManifest": "common/blocks-library/blocks.json",
        "blocksThemes": "common/blocks-library/blocks-themes.json",
        "localBlocks": "common/blocks",
        "componentsFilename": "components.json",
        "componentsManifest": "common/components/components.json",
        "componentsThemes": "common/components/components-themes.json",
        "localComponents": "common/components",
        "modulesFilename": "modules.json",
        "modulesManifest": "common/blocks-library/modules.json",
        "bundle": "build/dev/app.js",
        "rootComponent": "App.vue",
        "slides": "slides",
        "themes": "themes",
        "themePaths": {
            "variables": "theme.scss",
            "variablesJson": "theme.json",
            "main": "index.scss"
        },
        "themesManifest": "themes/themes.json",
        "settings": "settings.json",
        "icon": "icon.png",
        "icon2x": "icon@2x.png",
        "preview": "preview.jpg",
        "assets": ".ewizard/assets.json",
        "documents": "documents.json",
        "layouts": "layouts",
        "slide": {
            "thumbnail": "media/images/thumb.jpg",
            "screenshot": "media/images/screenshot.jpg"
        },
        "common": {
            "i18n": "common/i18n",
            "references": "common/resources/references.json",
            "claims": "common/resources/claims.json",
            "footnotes": "common/i18n/footnotes.json",
            "media": {
                "images": "common/media/images",
                "videos": "common/media/videos",
                "pdfs": "common/media/pdfs",
                "fonts": "common/media/fonts"
            },
            "triggeredEmailManifest": "common/resources/triggeredEmail.json"
        },
        "metadata": {
            "purpose": "common/metadata/purpose.json",
            "targetMessenger": "common/metadata/targetMessenger.json"
        },
        "icons": {
            "blocks": "common/icons/blocks"
        }
    },
    "archive": {
        "ignore": []
    },
    "cli": {
        "identifyComponents": true,
        "npm": {
            "version": "latest"
        }
    },
    "template": {
        "url": "https://git.qapint.com/ewizardjs/templates/email",
        "version": "8daa61780bc40aa7516f3fd09e5b8454ee4eb6e5"
    }
}
```

- `content.type`
- `content.subtype`
- `screenshoter.slideWithCommonLayout` - **eDatailer**
- `path.blocks`
- `path.blocksFilename` - yазва файлу, який визначає, які блоки відображаються на панелі елементів у редакторі eWizard.
- `path.blocksManifest` - шлях до файлу, який визначає, які блоки відображаються в редакторі eWizard.
- `path.blocksThemes` - шлях до файлу, де можна налаштувати, які блоки потрібно відображати для конкретної теми на вкладці "Блоки" у редакторі eWizard.
- `path.localBlocks`
- `path.componentsFilename` - назва файлу, який визначає, які компоненти відображаються на панелі елементів у редакторі eWizard.
- `path.componentsManifest`
- `path.componentsThemes`
- `path.localComponents`
- `path.modulesFilename`
- `path.modulesManifest` - **Classic**
- `path.bundle` - шлях до файлу з розробчою версією.
- `path.rootComponent` - кореневий файл, де ви редагуєте макет основної шаблонної сторінки.
- `path.slides` - **eDetailer**
- `path.themes`
- `path.themePaths.variables` - назва файлу з динамічними стилями тем. Кожна тема має свій файл.
- `path.themePaths.variablesJson` - назва файлу з динамічними змінними тем. Кожна тема має свій файл.
- `path.themePaths.main` - основний файл з динамічними стилями теми. Кожна тема має свій файл.
- `path.themesManifest` - шлях до файлу, який визначає, які теми використовуються в проекті.
- `path.settings`
- `path.icon`
- `path.icon2x`
- `path.preview` - назва файлу з попереднім переглядом проекту. Зображення генерується при завантаженні шаблону в NaviGate, запуску попереднього перегляду екрану wiz або ви можете створити його вручну.
- `path.assets`
- `path.claims`
- `path.documents` - шлях до файлу, який визначає, які документи експортуються у форматі PDF
- `path.layouts` - каталог з шаблонами електронної пошти.
- `path.slide.thumbnail` - шлях до файлу з мініатюрами.
- `path.slide.screenshot` - шлях до файлу з знімком екрану.
- `path.common.i18n` - каталог з локалізацією вмісту.
- `path.common.media.images`
- `path.common.media.videos`
- `path.common.media.pdfs`
- `path.common.media.fonts`
- `path.common.triggeredEmailManifest` - **eDetailer**
- `path.common.references` - шлях до файлу, який визначає, які посилання з'являються в редакторі eWizard.
- `path.metadata.purpose` - шлях до файлу, де зберігаються цілі.
- `path.metadata.targetMessenger` - шлях до файлу з налаштуваннями цільових месенджерів для рекламних оголошень у месенджерах.
- `path.icons.blocks` - шлях до створених ікон блоків. 
- `archive.ignore` - використовуйте масив для виключення розміток з архіву.
- `cli.identifyComponents` - коли значення встановлено на `true` , запуск `wiz archive` додає атрибут `data-asset-id` до всіх компонентів eWizard, Vue та HTML у файлі `App.vue` шаблону. Типовим значенням є `false`.
- `cli.npm.version` - версія npm, яка впливає на команди `wiz install` та `wiz uninstall`. Доступні варіанти: `latest` або `legacy` . За замовчуванням або якщо опція не налаштована у шаблоні, eWizard вибирає версію на основі залежностей `package.json`.
- `template.url` - лінк до репозиторію з електронною поштою.
- `template.version` - версія шаблону email, створеного після ініціалізації електронної пошти.


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