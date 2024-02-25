---
share: true
---
## Установка и настройка локального Obsidian

1) Скачать и установить Git https://git-scm.com/download/win
2) Скачать и установить Obsidian https://obsidian.md/
3) Создать локальный Vault в любом месте на своем компьютере
4) Открыть настройки [[Obsidian_setting_button.png|Obsidian_setting_button.png]]
5) Перейти в Community Plugins и включить их [[Obsidian_community_plugins_turn_on.png|Obsidian_community_plugins_turn_on.png]]
6) Перейти в список через кнопку Browse [[Obsidian_community_plugins_browse.png|Obsidian_community_plugins_browse.png]]
7) Найти плагин Github Publisher [[Obsidian_Github_Publisher.png|Obsidian_Github_Publisher.png]]
8) Установить его [[Obsidian_Github_Publisher_install.png|Obsidian_Github_Publisher_install.png]]
9) Включить плагин [[Obsidian_Github_Publisher_enable.png|Obsidian_Github_Publisher_enable.png]]
10) Перейти в настройки плагина и импортировать настройки [[Obsidian_Github_Publisher_import_settings.png|Obsidian_Github_Publisher_import_settings.png]]
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
10) Самостоятельно ввести настройки [[Obsidian_Github_Publisher_install_github_config.png|GitHub config]]:
    GitHub username: plusmedia
    Repository name: doc
    GitHub token: [Нужно сгенерировать на GitHub](https://github.com/settings/tokens/new?scopes=repo,workflow)

11) Таким же образом найти, установить и включить плагин [[Obsidian_Git.png|Git]]
12) Отрыть ввод команд [[Obsidian_open_command_palette.png|Obsidian_open_command_palette.png]]
13) Выбрать команду [[Obsidian_git_clone.png|Git: Clone an existing remote repo]]
14) Ввести URL https://github.com/Plusmedia/doc.git

![[Obsidian_Github_Publisher_enable.png|Obsidian_Github_Publisher_enable.png]]