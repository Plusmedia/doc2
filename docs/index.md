---
share: true
---
## Установка и настройка локального Obsidian

1) Скачать и установить Git https://git-scm.com/download/win
2) Зайти в любую папку, где будет храниться документация
3) В адресной строке ввести `cmd` ![[cmd.png]]
4) Откроется консоль, где нужно ввести
```
git clone https://github.com/Plusmedia/doc.git
```
![[git_clone.png]]
5) Скачать и установить Obsidian https://obsidian.md/
6) Запустить Obsidian и выбрать вариант [[Obsidian_open_folder.png|Open folder as vault]]
7) Указать папку куда был склонирована документация [[Obsidian_folder.png]]
8) Открыть настройки [[Obsidian_setting_button.png]]
9) Перейти в Community Plugins и включить их [[Obsidian_community_plugins_turn_on.png]]
10) Перейти в список через кнопку Browse [[Obsidian_community_plugins_browse.png]]
11) Найти плагин [[Obsidian_git.png|Git]]
12) [[Obsidian_git_install.png|Установить плагин Git]]
13) [[Obsidian_git_enable.png|Включить плагин Git]]
14) В настройках плагина можно включить Pull updates on startup
15) Отрыть ввод команд ![[Obsidian_open_command_palette.png]]
16) Ввести [[git_pull.png|Git pull]] чтобы убедиться, что [[git_pull_ok.png|все работает]]
17) После внесения изменений в документацию нужно вводить команду [[git_commit.png|Git commit all changes]]
18) Чтобы залить документацию на сервер нужно ввести [[git_push.png|Git push]]
19) Все настройки Obsidian индивидуальные, поэтому они не залиты в репозиторий. Для всех команд описанных выше можно настроить хоткеи по желанию ![[Obsidian_hotkeys.png]]

### Github Publisher (альтернативная заливка файлов, сейчас не используется)
1) Найти плагин Github Publisher [[Obsidian_Github_Publisher.png]]
2) Установить его [[Obsidian_Github_Publisher_install.png]]
3) Включить плагин [[Obsidian_Github_Publisher_enable.png]]
4) Перейти в настройки плагина и импортировать настройки [[Obsidian_Github_Publisher_import_settings.png]]
```{
  "github": {
    "branch": "main",
    "automaticallyMergePR": true,
    "dryRun": {
      "enable": false,
      "folderName": "github-publisher"
    },
    "tokenPath": "%configDir%/plugins/%pluginID%/env",
    "api": {
      "tiersForApi": "Github Free/Pro/Team (default)",
      "hostname": ""
    },
    "workflow": {
      "commitMessage": "[PUBLISHER] Merge",
      "name": ""
    },
    "verifiedRepo": true
  },
  "upload": {
    "behavior": "obsidian",
    "defaultName": "docs",
    "rootFolder": "",
    "yamlFolderKey": "",
    "frontmatterTitle": {
      "enable": false,
      "key": "title"
    },
    "replaceTitle": [],
    "replacePath": [],
    "autoclean": {
      "enable": false,
      "excluded": []
    },
    "folderNote": {
      "enable": false,
      "rename": "index.md",
      "addTitle": {
        "enable": false,
        "key": "title"
      }
    },
    "metadataExtractorPath": ""
  },
  "conversion": {
    "hardbreak": false,
    "dataview": true,
    "censorText": [],
    "tags": {
      "inline": false,
      "exclude": [],
      "fields": []
    },
    "links": {
      "internal": false,
      "unshared": false,
      "wiki": false,
      "slugify": "disable"
    }
  },
  "embed": {
    "attachments": true,
    "overrideAttachments": [],
    "keySendFile": [],
    "notes": false,
    "folder": "",
    "convertEmbedToLinks": "keep",
    "charConvert": "->",
    "useObsidianFolder": true
  },
  "plugin": {
    "shareKey": "share",
    "excludedFolder": [],
    "copyLink": {
      "enable": false,
      "links": "",
      "removePart": [],
      "transform": {
        "toUri": true,
        "slugify": "lower",
        "applyRegex": []
      }
    },
    "setFrontmatterKey": "Set"
  }
}
```
5) Самостоятельно ввести настройки [[Obsidian_Github_Publisher_install_github_config.png|GitHub config]]:
    GitHub username: plusmedia
    Repository name: doc
    GitHub token: [Нужно сгенерировать на GitHub](https://github.com/settings/tokens/new?scopes=repo,workflow)

## Структура папок

- docs - где хранятся все заметки
  - assets - место для файлов
  - hidden - заметки отсюда не выводятся на сайт
  - notes и любые другие папки - меню на сайте
  - файл index - этот файл, главная сайта
  - любые другие файлы - меню на сайте
- overrides - служебная папка для веба
- README документ для github