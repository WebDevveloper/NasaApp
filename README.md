# NasaApp — Astronomy Picture of the Day (React + Vite)

**Status:** Maintained / polishing.

**Next:** deploy + screenshots (Netlify/Vercel).

**Кратко (30 сек):** одностраничное приложение, которое подтягивает **APOD** (Astronomy Picture of the Day) из публичного NASA API и показывает полноразмерное изображение с заголовком/датой/описанием в боковой панели.

## Демо / скриншоты
- Деплой: coming soon
- Скриншоты: `./docs/screenshots/` (главный экран + боковая панель + Lighthouse mobile)

## Стек
- **Frontend:** React 18, Vite 5, JSX, CSS
- **UI:** Google Fonts (Inter), иконки — Font Awesome (CDN)
- **Состояние:** `useState` + `useEffect`
- **Данные:** NASA APOD (через `fetch`), ключ в `.env`
- **Качество:** ESLint

## Фичи (то, что есть сейчас)
- Загрузка сегодняшнего **APOD** (изображение `hdurl`, заголовок `title`)
- Просмотр **даты** и **описания (`explanation`)** в выезжающей боковой панели
- Кнопка/иконка для открытия/закрытия панели (шестерёнка / стрелка)
- Базовая индикация загрузки (стейт `loading`)

> Примечание: приложение использует ключ среды `VITE_NASA_API_KEY`. Находится в файле `.env` (см. ниже).

## Архитектура (фактическая)
```
src/
  components/
    Main.jsx     # фон/изображение APOD (data.hdurl, alt=data.title)
    Footer.jsx   # заголовок/кнопка открытия панели
    SideBar.jsx  # боковая панель: title, date, explanation
  App.jsx        # загрузка данных, состояния loading/showModal
  index.css
  main.jsx
index.html        # lang="en", Google Fonts + Font Awesome
vite.config.js
```

## Переменные окружения
Был создан `./.env` в корне проекта:
```bash
VITE_NASA_API_KEY=your_api_key_here
```
> Получить ключ можно на api.nasa.gov (бесплатно). В коде он доступен как `import.meta.env.VITE_NASA_API_KEY`.

## Метрики (цели для мобильных)
- Lighthouse: **90–100**
- Web Vitals: **LCP < 2.0 s**, **CLS ~ 0.01**
- Bundle: **≤ 300 KB**
> Скриншоты с Lighthouse положи в `./docs/screenshots/`.

## Доступность (A11y)
- Клавиатурная навигация и видимые фокусы
- Альтернативный текст для изображения (`alt={data.title || 'bg-img'}`)
- Рекомендуется добавить ARIA для кнопок открытия/закрытия панели

## Roadmap
- [ ] Обработка 4xx/5xx и пустых состояний (ошибка сети, лимит API)
- [ ] Дата-пикер для выбора APOD за прошедшие дни
- [ ] Lazy-loading изображений + prefetch метаданных
- [ ] Локализация RU/EN (title/labels), переключатель языка
- [ ] Скриншоты и отчёт метрик Lighthouse
- [ ] (опц.) Перевод на TypeScript, вынос API в `src/services/nasa.js`

## Цель проекта
Показать работу с внешним API (NASA APOD) на чистом React/Vite: загрузка данных, управление состоянием, грамотный UI (боковая панель), и оформить репозиторий как «витрину» для портфолио.

## Запуск
```bash
npm i
npm run dev        # http://localhost:5173
npm run build
npm run preview
```
