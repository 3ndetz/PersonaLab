# Minecraft 1.21 + моды

## 1️⃣ Установка Java

**ОБЫЧНО НЕ ТРЕБУЕТСЯ!**
*Пропускайте шаг и возвращайтесь, только если не запускается лаунчер, но обычно он предложит вам нужную версию сам!*

**Требуется:** Java 21

- **Windows/Linux:** [Oracle JDK 21](https://www.oracle.com/java/technologies/downloads/#java21) или [Adoptium](https://adoptium.net/)
- **Проверка:** Открыть терминал и выполнить `java -version`

## 2️⃣ Установка Minecraft

Скачайте и установите майнкрафт любым удобным способом, для ознакомления со способами есть такой [гайд](https://cq.ru/articles/gaming/kak-skachat-minecraft-na-pk).

Когда запустите лаунчер и будет выбор версии, обратите внимание на версию!

Если отображаются мод-системы (например, 1.21 Fabric) - значит, выбирайте сразу Fabric

**Версия:** **Minecraft 1.21** (НЕ 1.21.1, НЕ 1.21.X, НЕ 1.20!)

## 3️⃣ Установка Fabric

*Пропустите шаг, если уже в лаунчере выбрали версию 1.21 Fabric! Если просто 1.21 (без Fabric), то делайте этот шаг.*

**Fabric** — система модов для Minecraft

1. Скачать [Fabric Installer](https://fabricmc.net/use/installer/)
2. Запустить, выбрать версию **1.21**
3. Нажать Install
4. В лаунчере появится профиль **Fabric 1.21**

Запустите игру для теста.

Запомните ПАПКУ установки самой игры (НЕ ЛАУНЧЕРА!).

Папка игры обычно находится здесь:

- **Windows:** `%appdata%\.minecraft\mods`
- **Linux:** `~/.minecraft/mods`

Чтобы узнать папку игры точно, можно зайти в игру, нажать Options (Настройки) → Resource Packs (Ресурс-паки) → Open Pack Folder (Открыть папку с паками) → подняться на уровень выше (из папки resourcepacks) → вы в папке игры!

## 4️⃣ Установка модов

### Основной мод: AutoClef

1. Скачать [последний релиз AutoClef](https://github.com/3ndetz/autoclef/releases/latest)
2. Поместить `.jar` файл в папку `mods` игры:

Запомните путь к конфиг-файлам: `папка игры/altoclef/`

### Необходимые моды

Ссылки на ModRinth, нужно везде выбрать Fabric 1.21 в версиях:

- Cloth config
- IAS (Ingame Account Switcher)
- ModMenu
- No Peeking
- OkZoomer
- [Fabric API](https://modrinth.com/mod/fabric-api/version/oGwyXeEI)
- VoiceChat
- NoСhatReports

### Дополнительные моды (опционально)

Для оптимизации:

- FerriteCore
- ModernFix

полезные утилиты для стримеров:

- ChatPlus
- ReplayMod

для улучшенных визуалов:

- NotEnoughAnimations
- Physics Mod
- Player Animation Lib Fabric
- Architectury
- Entity Model Features
- Entity Texture Features
- Fabric Language Kotlin
- FirstPerson

## 5️⃣ Подключение к серверу

1. Запустить Minecraft 1.21 Fabric
2. Multiplayer → Add Server
3. Ввести адрес сервера интенсива
4. Зарегистрироваться: `/register <пароль> <пароль>`
5. Войти: `/login <пароль>`

## 6️⃣ Команды

### Команды сервера

- `/spawn` — телепорт на спаун
- `/tpa <ник>` — запрос телепортации к игроку
- `/tell <ник> <сообщение>` — личное сообщение

### Команды бота (AutoClef)

- `@stop` — остановить текущую задачу
- `@punk` — режим свободного поведения
- `@game` — игровой режим
- `@help` — список всех команд

## 7️⃣ Voice Chat + TTS

**Настройка голосового чата:**

1. Установить мод [Simple Voice Chat](https://modrinth.com/plugin/simple-voice-chat)
2. В настройках игры: Options → Voice Chat Settings
3. Выбрать виртуальный аудиокабель как устройство вывода
4. Подключить к TTS-системе стримерши

## Дополнительно: конфиг-файлы AutoClef

На этапе установке вы запомнили папку для конфигов, немного пройдёмся по важным настройкам:

`altoclef/configs/butler.json`:

- multiplayer_password` - можно указать свой пароль который игрок регает на серверах через /register, чтобы оно могло заходить само.

ну и в целом там есть важные ещё конфиги, например:

- `altoclef_settings.json/mobDefense` можно отключить автоматическую защиту от мобов и т.д., там много всего

В целом названия параметров обычно говорят сами за себя.
