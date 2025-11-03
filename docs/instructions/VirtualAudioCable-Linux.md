# 🔊 Настройка виртуального аудиокабеля (Linux)

> **Время:** 10–20 минут  
> **Роли:** Хост, DevOps

Виртуальный аудиокабель позволяет направлять звук между приложениями без физического кабеля. Это необходимо для TTS-озвучки в стриме.

---

## 📥 Установка PulseAudio

```bash
# Ubuntu/Debian
sudo apt update
sudo apt install pulseaudio pulseaudio-utils pavucontrol

# Fedora
sudo dnf install pulseaudio pulseaudio-utils pavucontrol

# Arch Linux
sudo pacman -S pulseaudio pavucontrol
```

---

## ⚙️ Создание виртуального кабеля

### Метод 1: Временное создание (до перезагрузки)

Быстрый способ для тестирования:

```bash
# Создать виртуальный выход
pactl load-module module-null-sink sink_name=Virtual_Sink sink_properties=device.description=Virtual_Sink

# Создать виртуальный вход
pactl load-module module-remap-source source_name=Virtual_Mic master=Virtual_Sink.monitor source_properties=device.description=Virtual_Mic
```

### Метод 2: Постоянное создание (сохраняется после перезагрузки)

Для использования на постоянной основе:

1. Создайте/откройте файл конфигурации:

```bash
mkdir -p ~/.config/pulse
nano ~/.config/pulse/default.pa
```

2. Добавьте в конец файла:

```bash
# Виртуальный динамик
load-module module-null-sink sink_name=Virtual_Sink sink_properties=device.description=Virtual_Sink

# Виртуальный микрофон
load-module module-remap-source source_name=Virtual_Mic master=Virtual_Sink.monitor source_properties=device.description=Virtual_Mic
```

3. Сохраните файл:
   - Нажмите `Ctrl+O`, затем `Enter` для сохранения
   - Нажмите `Ctrl+X` для выхода

4. Перезапустите PulseAudio:

```bash
pulseaudio -k
pulseaudio --start
```

---

## 🎵 Использование через pavucontrol (графический интерфейс)

`pavucontrol` — удобный графический инструмент для управления звуком.

1. Запустите приложение:

```bash
pavucontrol
```

2. Перейдите на вкладку **"Воспроизведение"** (Playback)
3. Найдите ваше TTS-приложение в списке
4. В выпадающем меню рядом с ним выберите **"Virtual_Sink"**

### Настройка OBS:

1. В OBS: **Настройки** → **Аудио**
2. Добавьте источник **"Monitor of Virtual_Sink"**

> 💡 **Подробнее об OBS:** [OBS.md](./OBS.md)

---

## 🎧 Прослушивание (loopback)

Чтобы слышать звук из Virtual_Sink в своих наушниках:

```bash
pactl load-module module-loopback latency_msec=1 source=Virtual_Sink.monitor sink=@DEFAULT_SINK@
```

Параметр `latency_msec=1` минимизирует задержку.

### Отключение loopback:

```bash
pactl unload-module module-loopback
```

---

## 🎭 Настройка VTube Studio для lipsync

В VTube Studio:

1. Откройте настройки → **"Microphone"**
2. Выберите **"Monitor of Virtual_Sink"** или **"Virtual_Mic"**
3. Включите **"Microphone lipsync"** → **ON**

Теперь губы модели будут двигаться под TTS-озвучку!

> 💡 **Подробнее о VTube Studio:** [VtubeModel.md](./VtubeModel.md)

---

## 🔧 Проверка работы

### Просмотр доступных устройств:

```bash
# Список выходов (sinks)
pactl list sinks short

# Список входов (sources)
pactl list sources short
```

Вы должны увидеть `Virtual_Sink` в списке выходов.

### Проверка загруженных модулей:

```bash
pactl list modules | grep -E "(null-sink|remap-source)"
```

---

## ❓ Частые проблемы

### Не работает виртуальный кабель
```bash
# Проверьте статус PulseAudio
pulseaudio --check

# Если не работает, перезапустите
pulseaudio -k
pulseaudio --start
```

### Модули не загружаются
```bash
# Убедитесь, что модули загружены
pactl list modules

# Проверьте конфигурационный файл
cat ~/.config/pulse/default.pa
```

### Нет звука в OBS
- Убедитесь, что в pavucontrol выбран правильный источник
- Проверьте, что TTS направлен на Virtual_Sink
- Перезапустите OBS

### Звук с задержкой
```bash
# Уменьшите задержку loopback
pactl unload-module module-loopback
pactl load-module module-loopback latency_msec=1 source=Virtual_Sink.monitor sink=@DEFAULT_SINK@
```

---

## 🚀 Альтернатива: PipeWire

На современных дистрибутивах (Ubuntu 22.04+, Fedora 34+) может использоваться **PipeWire** вместо PulseAudio.

### Создание виртуального кабеля в PipeWire:

```bash
pw-loopback -m '[ FL FR ]' --capture-props='media.class=Audio/Sink node.name=virtual_sink' &
```

### Проверка:

```bash
pw-cli list-objects | grep node.name
```

> 💡 PipeWire совместим с командами PulseAudio через `pactl`

---

## 🔗 Полезные ссылки

- [PulseAudio Documentation](https://www.freedesktop.org/wiki/Software/PulseAudio/)
- [PipeWire Official](https://pipewire.org/)
- [Arch Wiki: PulseAudio](https://wiki.archlinux.org/title/PulseAudio)
- **Для Windows:** [VirtualAudioCable-Windows.md](./VirtualAudioCable-Windows.md)
