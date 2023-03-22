## настраиваем stylelint

Установим все необходимые пакеты:
stylelint — сам линтер,
stylelint-scss — плагин для работы с .scss файлами,
stylelint-config-standard — стандартный конфиг для stylelint, который включает в себя стайл гайд AirBnB и другие общепринятые принципы,
stylelint-order — плагин для проверки порядка свойств,
prettier — Prettier для форматирования кода,
stylelint-prettier — для форматирования кода с помощью Prettier,
stylelint-config-prettier-scss — Отключает все правила CSS и SCSS, которые не нужны или могут конфликтовать с Prettier,
stylelint-config-rational-order — Конфигурация Stylelint, которая сортирует связанные объявления свойств, группируя их в определенном порядке.

Настроим конфиг для stylelint, для этого создаем файл .stylelintrc.json

Чтобы VS Code подсвечивал ошибки в стилях в соответствии с конфигурацией stylelint, надо установить плагин stylelint в VS Code, а так же добавить настройки для рабочей области в VS Code .vscode/settings.json:

```json
{
  "scss.validate": false,
  "css.validate": false,
  "less.validate": false,

  "editor.codeActionsOnSave": {
    "source.fixAll.stylelint": true
  },

  "stylelint.validate": ["css", "scss"]
}
```

Когда live sass compiler запущен и нажать ctrl+S, то ошибки сами пофиксятся.
НО! В style.css кое-какие блоки переносятся без пробела и тогда в конце всего нужно это пофиксить npm run stylelint:fix

Для запуска линтинга css файлов в проекте добавим новые скрипты в package.json

```json
"scripts": {
  "stylelint": "stylelint ./assets/css",
  "stylelint:fix": "stylelint ./assets/css --fix"
}
```

Команда npm run stylelint запустит линтер и выведет в консоль список ошибок, а npm run stylelint:fix дополнительно исправит ошибки, доступные для автоисправления.

## в VScode подключаем плагин live sass compiler

заводим структуру папок для верстки :
index.html
assets/
css/
js/
images/

В корне заводим папку scss. В ней файл с style.scss (такое же название будет у css-файла)

Внизу VSCode настройки -> в поравом верхнем углу (2строка) open setting json и вниз файла добавляем запись

```json
    //liveSassCompile выходной css
    "liveSassCompile.settings.generateMap": false,
    "liveSassCompile.settings.formats": [
      {
        "format": "expanded",
        "extensionName": ".css",
        "savePath": "~/../assets/css/"
      }
    ],
    "liveSassCompile.settings.autoprefix": ["> 1%", "last 10 versions"],
    // "liveSassCompile.settings.showOutputWindow": true,
    "liveServer.settings.AdvanceCustomBrowserCmdLine": ""
```

как будет заведен scss-файл внизу в панели VSCode появится надпись watch sass. Жмем на нее, чтобы запустить компиляцию
