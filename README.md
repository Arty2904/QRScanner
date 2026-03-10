# Сканер QR | QR Scanner

Android-приложение для сканирования и создания QR кодов.

## Стек технологий

| Слой | Технология |
|------|-----------|
| Язык | Kotlin |
| UI | XML Views + ViewBinding |
| Архитектура | MVVM + Repository |
| DI | Hilt |
| БД | Room (SQLite) |
| Камера | CameraX |
| Распознавание | ML Kit Barcode Scanning |
| Генерация QR | ZXing Core |
| Навигация | Navigation Component |
| Async | Kotlin Coroutines + Flow |

## Структура проекта

```
app/
├── data/
│   ├── db/
│   │   ├── AppDatabase.kt          — Room база данных
│   │   ├── ScanRecordDao.kt        — DAO (запросы)
│   │   └── ScanRecordEntity.kt     — Entity таблицы
│   └── repository/
│       └── ScanRepository.kt       — Репозиторий
├── domain/
│   └── model/
│       └── ScanRecord.kt           — Доменная модель
├── ui/
│   ├── scan/
│   │   ├── ScanFragment.kt         — Экран сканирования
│   │   ├── ScanViewModel.kt        — ViewModel
│   │   └── QrCodeAnalyzer          — ML Kit анализатор
│   ├── create/
│   │   ├── CreateFragment.kt       — Экран создания QR
│   │   ├── CreateViewModel.kt      — ViewModel + ZXing
│   │   └── QrResultBottomSheet.kt  — Модальное окно с QR
│   └── history/
│       ├── HistoryFragment.kt      — Экран истории
│       ├── HistoryViewModel.kt     — ViewModel
│       └── HistoryAdapter.kt       — RecyclerView адаптер
├── AppModule.kt                    — Hilt DI модуль
├── MainActivity.kt                 — Главная активность
└── QRScannerApp.kt                 — Application класс
```

## Функциональность

### Сканирование
- Сканирование QR кодов через камеру в реальном времени (ML Kit)
- Виброотклик при успешном сканировании
- Управление вспышкой
- Автоматическое определение типа: URL, WiFi, Email, Phone, SMS, Text
- Открыть / Копировать / Поделиться результатом
- Кнопка перехода в историю с счётчиком

### Создать QR
- Ввод до **2048 символов**
- Прогресс-бар символов с предупреждением
- Выбор типа: Текст / URL / WiFi / Email
- Bottom Sheet с готовым QR кодом (82% экрана)
- Сохранить PNG в галерею
- Поделиться изображением

### История
- Хранение до **100 записей** в Room DB
- Автоматическое удаление старых при превышении лимита
- Свайп влево для удаления записи
- Кнопка копирования у каждой записи
- URL-ссылки кликабельны (открываются в браузере)
- Относительное время (только что / 2 мин / 1 ч / вчера)
- Кнопка «Очистить всё» с подтверждением

## Установка и запуск

### Требования
- Android Studio Hedgehog (2023.1.1) или новее
- JDK 17
- Android SDK 34
- Минимальная версия Android: 7.0 (API 24)

### Шаги

1. Открой проект в Android Studio:
   ```
   File → Open → выбери папку QRScanner
   ```

2. Синхронизируй Gradle:
   ```
   File → Sync Project with Gradle Files
   ```

3. Запусти на устройстве или эмуляторе:
   ```
   Run → Run 'app'  (Shift+F10)
   ```

> **Важно:** для сканирования нужно реальное устройство с камерой.  
> Эмулятор поддерживает генерацию QR, но не сканирование.

### Разрешения
- `CAMERA` — запрашивается при первом открытии вкладки «Сканировать»
- `VIBRATE` — без запроса (normal permission)

## Минимальные требования к устройству
- Android 7.0+ (API 24)
- Камера с автофокусом (рекомендуется)
- ~20 MB свободного места
