```html
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <title>Barcode Printing Service</title>
    <style>
        body {font-family: Arial, sans-serif; line-height: 1.6; max-width: 800px; margin: 20px auto; padding: 0 20px}
        h1, h2 {color: #2c3e50; border-bottom: 2px solid #3498db; padding-bottom: 5px}
        .section {background: #f9f9f9; padding: 15px; margin: 15px 0; border-radius: 5px; border: 1px solid #ddd}
        pre {background: #f4f4f4; padding: 10px; overflow-x: auto}
        code {background: #f4f4f4; padding: 2px 5px}
        ul {padding-left: 20px}
        .warning {color: #c0392b; background: #f2dede; padding: 10px; border-radius: 5px}
    </style>
</head>
<body>
    <h1>Служба печати штрихкодов</h1>

    <div class="section">
        <h2>Основные возможности</h2>
        <ul>
            <li>Поддержка USB HID-сканеров</li>
            <li>Работа с принтерами Xprinter XP-365B и ESC/POS-совместимыми</li>
            <li>Обработка специальных штрихкодов:
                <ul>
                    <li>J1-C1 (1 шт)</li>
                    <li>J1-C5 (5 шт)</li>
                    <li>J1-C10 (10 шт)</li>
                    <li>J1-C50 (50 шт)</li>
                </ul>
            </li>
            <li>Интеграция с CSV-базами поставщиков</li>
            <li>Автозапуск через systemd</li>
        </ul>
    </div>

    <div class="section">
        <h2>Поддерживаемое оборудование</h2>
        <h3>Сканеры:</h3>
        <ul>
            <li>Honeywell Voyager 1200g</li>
            <li>Zebra DS2208</li>
            <li>Другие HID-клавиатурные сканеры</li>
        </ul>
        
        <h3>Принтеры:</h3>
        <ul>
            <li>Xprinter XP-365B</li>
            <li>Любые ESC/POS-совместимые принтеры</li>
        </ul>
        <div class="warning">Не поддерживаются: графические принтеры без TSPL</div>
    </div>

    <div class="section">
        <h2>Алгоритм работы</h2>
        <ol>
            <li>Сканирование штрихкода</li>
            <li>Проверка типа кода:
                <ul>
                    <li>Специальный код → Установка количества печати</li>
                    <li>Товарный код → Поиск в базе CSV</li>
                </ul>
            </li>
            <li>Генерация PDF-этикетки</li>
            <li>Конвертация в TSPL-команды</li>
            <li>Отправка на печать</li>
        </ol>
    </div>

    <div class="section">
        <h2>Установка и настройка</h2>
        
        <details>
            <summary><strong>Шаг 1: Установка зависимостей</strong></summary>
            <pre><code>sudo apt-get update
sudo apt-get install python3-dev python3-pip libjpeg-dev zlib1g-dev
pip3 install -r requirements.txt</code></pre>
        </details>

        <details>
            <summary><strong>Шаг 2: Настройка сервиса</strong></summary>
            <pre><code>sudo cp configs/barcode.service /etc/systemd/system/
sudo systemctl daemon-reload
sudo systemctl enable barcode.service</code></pre>
        </details>

        <details>
            <summary><strong>Шаг 3: Конфигурация</strong></summary>
            <pre><code>sudo mkdir /etc/barcode_service
sudo cp configs/config.ini.example /etc/barcode_service/config.ini
sudo nano /etc/barcode_service/config.ini</code></pre>
        </details>
    </div>

    <div class="section">
        <h2>Управление сервисом</h2>
        <pre><code># Запуск сервиса
sudo systemctl start barcode.service

# Проверка статуса
systemctl status barcode.service

# Просмотр логов
journalctl -u barcode.service -f</code></pre>
    </div>

    <div class="section">
        <h2>Важные примечания</h2>
        <ul>
            <li>Убедитесь что принтер определился как <code>/dev/usb/lp0</code></li>
            <li>CSV-файлы должны использовать кодировку UTF-8</li>
            <li>Для русского текста установите шрифты:
                <pre><code>sudo apt-get install ttf-mscorefonts-installer</code></pre>
            </li>
        </ul>
    </div>
</body>
</html>
```
