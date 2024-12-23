## Витяг тексту з PDF:
- Використовується бібліотека pdfplumber для отримання тексту з PDF-документів.
- Видаляються заголовки, номери сторінок та інші небажані артефакти.
## Обробка тексту:
- Текст розбивається на розділи за допомогою розділювача.
- Виконується очищення тексту: видалення зайвих розривів рядків та нормалізація пробілів.
## Розділення на секції:
- Кожен розділ ділиться на менші секції, враховуючи максимальну кількість слів.
- Для кожної секції зберігається метаінформація (номер розділу та секції).
## Збереження секцій:
- Кожна секція зберігається в окремий текстовий файл для подальшої обробки.
## Семантичний пошук:
- Використовується HuggingFace для створення векторних представлень тексту (ембеддінгів).
- За запитом знаходяться релевантні секції шляхом оцінки схожості.
## Пошук BM25:
- Використовується бібліотека rank_bm25 для пошуку за ключовими словами.
- Дає змогу порівнювати результати семантичного пошуку з класичним пошуком за ключовими словами.
## Реранкінг результатів:
- Після виконання семантичного або BM25 пошуку використовується модель реранкінгу для оцінки важливості знайдених результатів.
- Застосовується модель BAAI/bge-reranker-v2-m3 для повторного ранжування документів.
## Генерація відповідей LLM:
- Інтеграція з мовною моделлю:
    - Застосовується Groq API для виклику мовної моделі (gemma-7b-it).
    - Запит передається разом із контекстом (або без нього) для генерації відповіді.
- Налаштування моделі:
    - Передбачено параметр temperature для контролю рівня варіативності відповідей.
    - Контекст для моделі генерується автоматично на основі релевантних секцій.
## Інтерактивний інтерфейс:
- Створення інтерфейсу за допомогою Gradio:
    - Користувач вводить запит, обирає метод пошуку та додаткові параметри (наприклад, використання реранкінгу або контексту).
    - Відображаються релевантні документи, їх метаінформація та відповідь від LLM.
- Параметри пошуку:
    - Доступні методи пошуку: семантичний (semantic), BM25 (bm25) або відсутність пошуку (no search).
    - Пошук можна покращити за допомогою реранкінгу результатів.
- Вивід результатів:
    - Відображаються текстові уривки з документа, їх оцінки (BM25 та реранкер), а також відповідь мовної моделі.
