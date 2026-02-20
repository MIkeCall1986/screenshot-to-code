# screenshot-to-code

A simple tool to convert screenshots, mockups and Figma designs into clean, functional code using AI. Now supporting Gemini 3 and Claude Opus 4.5!

https://github.com/user-attachments/assets/85b911c0-efea-4957-badb-daa97ec402ad

Supported stacks:

- HTML + Tailwind
- HTML + CSS
- React + Tailwind
- Vue + Tailwind
- Bootstrap
- Ionic + Tailwind
- SVG

Supported AI models:

- Gemini 3 Flash and Pro - Best models! (Google)
- Claude Opus 4.5 - Best model! (Anthropic)
- GPT-5.2, GPT-4.1 (OpenAI)
- Other models are available as well but we recommend using the above models.
- DALL-E 3 or Flux Schnell (using Replicate) for image generation

See the [Examples](#-examples) section below for more demos.

We have experimental support for taking a video/screen recording of a website in action and turning that into a functional prototype.

![google in app quick 3](https://github.com/abi/screenshot-to-code/assets/23818/8758ffa4-9483-4b9b-bb66-abd6d1594c33)

[Learn more about video here](https://github.com/abi/screenshot-to-code/wiki/Screen-Recording-to-Code).

[Follow me on Twitter for updates](https://twitter.com/_abi_).

## 🌍 Hosted Version

[Try it live on the hosted version (paid)](https://screenshottocode.com).

## 🛠 Getting Started

The app has a React/Vite frontend and a FastAPI backend.

Keys needed:

- [OpenAI API key](https://github.com/abi/screenshot-to-code/blob/main/Troubleshooting.md), Anthropic key, or Google Gemini key
- Multiple keys are recommended so you can compare results from different models

If you'd like to run the app with Ollama open source models (not recommended due to poor quality results), [follow this comment](https://github.com/abi/screenshot-to-code/issues/354#issuecomment-2435479853).

Run the backend (I use Poetry for package management - `pip install --upgrade poetry` if you don't have it):

```bash
cd backend
echo "OPENAI_API_KEY=sk-your-key" > .env
echo "ANTHROPIC_API_KEY=your-key" >> .env
echo "GEMINI_API_KEY=your-key" >> .env
poetry install
poetry shell
poetry run uvicorn main:app --reload --port 7001
```

You can also set up the keys using the settings dialog on the front-end (click the gear icon after loading the frontend).

Run the frontend:

```bash
cd frontend
yarn
yarn dev
```

Open http://localhost:5173 to use the app.

If you prefer to run the backend on a different port, update VITE_WS_BACKEND_URL in `frontend/.env.local`

## Docker

If you have Docker installed on your system, in the root directory, run:

```bash
echo "OPENAI_API_KEY=sk-your-key" > .env
docker-compose up -d --build
```

The app will be up and running at http://localhost:5173. Note that you can't develop the application with this setup as the file changes won't trigger a rebuild.

## 🙋‍♂️ FAQs

- **I'm running into an error when setting up the backend. How can I fix it?** [Try this](https://github.com/abi/screenshot-to-code/issues/3#issuecomment-1814777959). If that still doesn't work, open an issue.
- **How do I get an OpenAI API key?** See https://github.com/abi/screenshot-to-code/blob/main/Troubleshooting.md
- **How can I configure an OpenAI proxy?** - If you're not able to access the OpenAI API directly (due to e.g. country restrictions), you can try a VPN or you can configure the OpenAI base URL to use a proxy: Set OPENAI_BASE_URL in the `backend/.env` or directly in the UI in the settings dialog. Make sure the URL has "v1" in the path so it should look like this: `https://xxx.xxxxx.xxx/v1`
- **How can I update the backend host that my front-end connects to?** - Configure VITE_HTTP_BACKEND_URL and VITE_WS_BACKEND_URL in front/.env.local For example, set VITE_HTTP_BACKEND_URL=http://124.10.20.1:7001
- **Seeing UTF-8 errors when running the backend?** - On windows, open the .env file with notepad++, then go to Encoding and select UTF-8.
- **How can I provide feedback?** For feedback, feature requests and bug reports, open an issue or ping me on [Twitter](https://twitter.com/_abi_).

## 📚 Examples

**NYTimes**

| Original                                                                                                                                                        | Replica                                                                                                                                                         |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <img width="1238" alt="Screenshot 2023-11-20 at 12 54 03 PM" src="https://github.com/user-attachments/assets/6b0ae86c-1b0f-4598-a578-c7b62205b3e2"> | <img width="1414" alt="Screenshot 2023-11-20 at 12 59 56 PM" src="https://github.com/user-attachments/assets/981c490e-9be6-407e-8e46-2642f0ca613e"> |


**Instagram**

https://github.com/user-attachments/assets/a335a105-f9cc-40e6-ac6b-64e5390bfc21

**Hacker News**


https://github.com/user-attachments/assets/205cb5c7-9c3c-438d-acd4-26dfe6e077e5

20.02.26 sync fork
Ось результати аналізу та стратегія трансформації для проекту **screenshot-to-code**, підготовлені у форматі для копіювання в Notion.

---

# 📑 Звіт AI-консультанта: Проект "screenshot-to-code"

**screenshot-to-code** — це інтелектуальний інструмент, який перетворює скріншоти, макети та дизайни Figma у чистий, функціональний код за допомогою мультимодальних моделей ШІ.

---

## 🧬 Частина 1: "ДНК" Проекту

Логіку коду проекту можна розбити на такі **атомарні функції**:

*   **Парсинг візуальних вхідних даних:** Прийом зображень (скріншотів) або відеозаписів екрана для подальшого аналізу ШІ.
*   **Оркестрація мультимодальних LLM:** Інтеграція з провідними моделями, такими як **Gemini 1.5 Pro/Flash**, Claude 3.5 Sonnet та GPT-4o, через API-ключі.
*   **Генерація коду для різних стеків:** Перетворення візуальних образів у специфічні структури: **HTML + Tailwind, React, Vue, Bootstrap** або **Ionic**.
*   **Синтез зображень (DALL-E 3 / Flux):** Автоматичне створення реалістичних зображень-заповнювачів для згенерованого інтерфейсу.
*   **Живий рендеринг та прев'ю:** Взаємодія між бекендом на **FastAPI (Python)** та фронтендом на **React (TypeScript)** для миттєвого відображення результату.

### 💎 Головна технічна цінність
Головна цінність проекту полягає в **автоматизації переходу від дизайну до фронтенд-розробки**. Він усуває рутинну роботу з верстки, дозволяючи розробникам отримувати готові компоненти за лічені секунди, підтримуючи при цьому найсучасніші моделі ШІ для максимальної точності.

---

## 🚀 Частина 2: "Трансформація" (Інтеграція з Gemini LLM 2026)

Хоча проект вже підтримує Gemini, використання наступних поколінь моделей у парі з вашими скриптами перетворює його на **автономний дизайнерський департамент**.

### Як зміниться функціонал?
1.  **Семантичне редагування коду:** Gemini 2026 зможе не просто кодувати скріншот, а розуміти бізнес-логіку елементів (наприклад, "зроби цю кнопку функціональною для оплати через Stripe").
2.  **Відео-прототипування:** Покращена підтримка відео дозволить створювати складні анімації та переходи, просто записавши рухи курсору на макеті.
3.  **Голосове керування стилями:** Користувач зможе голосом коригувати згенерований код у реальному часі (наприклад: *"Додай неоновий ефект до всіх карток"*).

### Сценарій сервісу "Instant UI Service" (Project + Gemini + ID_{$})

Сценарій роботи готового сервісу на вашому сайті:
1.  **Моніторинг трендів (ID_{1}):** Ваш Python-скрипт **ID_{1}** щодня збирає скріншоти найкращих дизайнів з Dribbble або Awwwards.
2.  **Генерація компонентів (screenshot-to-code):** Зібрані скріншоти автоматично проходять через ядро проекту, де Gemini генерує для них код у форматі React + Tailwind.
3.  **Оптимізація та брендування (ID_{2}):** Скрипт **ID_{2}** автоматично замінює кольори та шрифти у згенерованому коді на ваші корпоративні стилі.
4.  **Публікація:** Готові компоненти автоматично потрапляють у бібліотеку вашого сайту для швидкого використання.
5.  **Деплой:** Використовуючи **GitHub Spark**, ви розгортаєте цей процес як інтелектуальний застосунок, де клієнти вашого сайту можуть просто завантажити фото свого начерку на папері та миттєво отримати готовий сайт.

---

## 📋 План дій для Notion
| Крок | Дія | Результат |
| :--- | :--- | :--- |
| **1** | Налаштування оточення через Docker | Готовий локальний сервер |
| **2** | Підключення **GEMINI_API_KEY** у `.env` | Доступ до найпотужніших моделей ШІ |
| **3** | Створення API-містка для скриптів `ID_{$}` | Автоматизація потоку дизайнів |
| **4** | Використання **GitHub Spark** для UI | Запуск сервісу для кінцевих користувачів |

---

### 💡 Резюме

**Суть:** **Перетворення зображень у чистий код**.

**AI-Роль:** **Створення інтелектуальних застосунків через Spark**.
