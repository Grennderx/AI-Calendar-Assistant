# AI Calendar Assistant

## Описание

AI Calendar Assistant — это интеллектуальный ассистент для работы с календарными событиями, который использует языковые модели для:

- Автоматического распознавания событий в текстовом вводе
- Извлечения структурированных данных о событиях
- Генерации подтверждений с ссылками на Google Calendar
- Обработки естественно-языковых запросов

## Основные функции

1. **Трехэтапная обработка событий**:
   - Извлечение базовой информации
   - Парсинг деталей события
   - Генерация подтверждения

2. **Поддержка естественного языка**:
   - Распознавание относительных дат ("next Thursday")
   - Обработка сложных списков участников
   - Автоматическое вычисление дат

3. **Интеграция с Google Calendar**:
   - Автогенерация ссылок для добавления событий
   - Корректное форматирование времени и дат

## Технологии

- Python 3.10+
- Pydantic (валидация данных)
- OpenAI API (через OpenRouter)
- LM Studio (локальные модели)
- Логирование всех операций

## Установка

1. Установите зависимости:
```bash
pip install openai python-dotenv pydantic
```

2. Для использования по API создайте файл `.env` с вашим API-ключом:
```
OPENROUTER_API_KEY=your_api_key_here
```

3. Для локального использования (опционально):
- Установите LM Studio
- Загрузите модель `qwen2.5-coder-7b-instruct` (опционально)

## Использование

```python
from ai_calendar import process_calendar_request

# Пример запроса
result = process_calendar_request(
    "Let's schedule a 1.5h team meeting next Thursday at 3 pm with Vlad, Lionel Pepsi and Ghislen Konan"
)

if result:
    print(f"Confirmation: {result.confirmation_message}")
    print(f"Calendar link: {result.calendar_link}")
else:
    print("Invalid event request")
```

## Пример вывода

```
Confirmation: Confirmed: Team Meeting on 2025-08-15 at 3 PM (1.5 hours) with Vlad Vasilev, Lionel Pepsi, Ghislen Konan
Calendar link: https://www.google.com/calendar/render?action=TEMPLATE&text=Team%20Meeting&dates=20250815T150000Z/20250815T163000Z
```

## Особенности реализации

1. **Строгая валидация данных**:
   - Проверка сохранения оригинальных имен участников
   - Контроль форматов дат и времени
   - Валидация confidence score

2. **Гибкая настройка**:
   - Возможность использования как облачных, так и локальных моделей
   - Настраиваемые пороги confidence score
   - Подробное логирование всех этапов

3. **Безопасность**:
   - Защита от подмены данных
   - Явные предупреждения о любых изменениях
   - Запрет на додумывание информации
