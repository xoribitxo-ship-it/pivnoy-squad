# AGENTS.md

Одностраничный статический сайт Minecraft-сервера «Пивной Сквад».
Живой адрес: https://pivnoy-squad.vercel.app/

## Главное

- **Нет сборки и фреймворка.** Рядом с `index.html` всегда правь сам `index.html`: HTML, CSS и JS темы лежат в нём инлайн. Не добавляй Vite/React без явного запроса.
- **Не заменяй графику.** Иллюстрация таверны — CSS-арт (полки, бутылки, фигурки, кружки), а не изображение. Скины — реальные файлы из проекта; не подставляй стоковые картинки.
- Скин MoreThanSkill вшит в HTML как base64. Его копия — `assets/skins/morethan-sprite.png`. Скин Undead_xD лежит в корне и грузится по `/undead-sprite.png` — этот путь зашит в разметке.
- Шрифты: `Press Start 2P` (Google Fonts) только для заголовков; основной текст — системный моноширинный стек. Не возвращай `Rubik Pixel(s)` для body: проверено, при 15px текст плохо читается.
- Тема хранится в `localStorage` (`ps-theme`), класс `dark` ставится на `<html>`; в CSS поэтому селекторы `html.dark body`, а не `body.dark`.

## Проверка

```powershell
npx --yes serve . -l 3000
```

Открыть http://localhost:3000. Автотестов нет; проверяй вручную светлую/тёмную тему, мобильную ширину ≤480px и кнопку копирования IP.

## Сеть

Внешний доступ на этой машине идёт через прокси `http://127.0.0.1:12334`. Для npm:

```powershell
$env:npm_config_proxy = "http://127.0.0.1:12334"
$env:npm_config_https_proxy = "http://127.0.0.1:12334"
```

Для git: `git config --global http.proxy http://127.0.0.1:12334`.

## Git и деплой

- Git — портативный, `C:\Users\user\AppData\Local\Programs\PortableGit2\cmd` (уже в PATH пользователя).
- Ветка `main`, коммиты короткие и по одной правке.
- Деплой на Vercel статикой. Не создавай новый проект Vercel молча: адрес `pivnoy-squad.vercel.app` должен сохраниться.
