# Настройка виртуального аудиокабеля для Linux

Текущие способы под Linux нормально не работают... Ищем нормальный способ.

<https://askubuntu.com/questions/633674/virtual-audio-cable-for-ubuntu>

Нужно настроить виртуальный кабель, который сможем запустить в Python. Вручную переназначать каждый раз через pavucontrol будет тяжко...

Экспериментальные способы, не проверены... Скорее всего скрипт с ними не заработает.

## **Самый простой способ для Linux - PulseAudio null sink:**

убедитесь что стоит pulse audio

```bash
sudo apt-get install pulseaudio-utils
```

### **1. Создать виртуальный аудио кабель (одной командой):**

```bash
# Создать виртуальное устройство
pactl load-module module-null-sink sink_name=virtual_cable sink_properties=device.description="Virtual_Cable"

# Создать monitor (это будет "выход" кабеля, который другие приложения видят как "микрофон")
# Monitor автоматически создаётся вместе с null sink!
```

### **2. Сделать постоянным (чтобы после перезагрузки оставалось):**

Добавить в `/etc/pulse/default.pa` или `~/.config/pulse/default.pa`:

```bash
load-module module-null-sink sink_name=virtual_cable sink_properties=device.description="Virtual_Cable"
```

### **3. Использование:**

**В вашем коде:**
- Устройство появится как `"Virtual_Cable"` или `"Monitor of Virtual_Cable"` в списке
- **Для вывода звука** → выбираете `"Virtual_Cable"` 
- **Для захвата звука** → выбираете `"Monitor of Virtual_Cable"`

**В других приложениях (OBS, Discord, etc.):**
- Выбираете `"Monitor of Virtual_Cable"` как источник микрофона
- Они будут слышать всё, что вы воспроизводите через `"Virtual_Cable"`

---

## **Проверка что создалось:**

```bash
pactl list short sinks          # Покажет ваш virtual_cable
pactl list short sources        # Покажет Monitor of Virtual_Cable
```

В Python они появятся в `sd.query_devices()` как обычные устройства!

**Итог:** Один sink = один виртуальный кабель. Можете создать несколько (для FX отдельный, например).
