# 🇷🇺 Русификация панели управления OpenClaw

Готовый набор файлов для добавления **русского языка** в **OpenClaw Control UI**.

---

## ✨ Что это даёт

После установки в панели управления OpenClaw появится:
- язык **Русский** в селекторе Language
- переведённая навигация
- русские подписи на основных экранах
- базовая русификация Overview / Chat / Cron / общих UI-элементов

---

## 📦 Что лежит в репозитории

```text
ui/src/i18n/locales/ru.ts   # файл русской локали
patches/registry.ts         # пример обновлённого registry.ts
patches/types.ts            # пример обновлённого types.ts
README.md                   # инструкция по установке
```

---

## 🧰 Требования

- установленный **OpenClaw**
- доступ к исходникам OpenClaw на сервере
- `pnpm` / рабочая сборка UI

Обычно исходники лежат примерно так:

```bash
/root/openclaw
```

---

## 🚀 Установка

### 1. Скопируйте файл локали

Скопируйте `ui/src/i18n/locales/ru.ts` в ваш OpenClaw:

```bash
cp ui/src/i18n/locales/ru.ts /root/openclaw/ui/src/i18n/locales/ru.ts
```

### 2. Обновите тип локали

Откройте файл:

```bash
/root/openclaw/ui/src/i18n/lib/types.ts
```

И добавьте `ru` в тип `Locale`:

```ts
export type Locale = "en" | "zh-CN" | "zh-TW" | "pt-BR" | "de" | "es" | "ru";
```

### 3. Обновите registry

Откройте файл:

```bash
/root/openclaw/ui/src/i18n/lib/registry.ts
```

Что нужно сделать:

#### Добавить `ru` в список lazy locales

```ts
const LAZY_LOCALES: readonly LazyLocale[] = ["zh-CN", "zh-TW", "pt-BR", "de", "es", "ru"];
```

#### Добавить `ru` в registry

```ts
ru: {
  exportName: "ru",
  loader: () => import("../locales/ru.ts"),
},
```

#### Добавить определение языка браузера

```ts
if (navLang.startsWith("ru")) {
  return "ru";
}
```

### 4. Добавьте русский в английский словарь

Откройте:

```bash
/root/openclaw/ui/src/i18n/locales/en.ts
```

И в блок `languages` добавьте:

```ts
ru: "Русский (Russian)",
```

### 5. Пересоберите UI

```bash
pnpm -C /root/openclaw ui:build
```

---

## ✅ Как включить русский язык

После сборки:

1. откройте панель управления OpenClaw
2. перейдите в **Overview**
3. найдите блок **Gateway Access**
4. в поле **Language** выберите **Русский**
5. если интерфейс не обновился — сделайте **Ctrl+F5**

---

## 🩹 Что уже переведено

- основная навигация
- вкладки
- Overview
- часть Chat
- общие подписи
- язык в селекторе
- часть Cron UI

---

## ⚠️ Ограничения

Это **не 100% тотальная русификация всего продукта**.

Что может остаться на английском:
- редкие технические строки
- часть глубоких экранов
- отдельные подписи в debug/logs/nodes/skills
- то, что ещё не вынесено в translation map

Но для повседневного использования панель уже становится заметно понятнее.

---

## 🔄 Откат

Если хотите вернуть всё назад:

1. удалите `ru.ts`
2. уберите `ru` из `types.ts`
3. уберите `ru` из `registry.ts`
4. уберите `ru` из `en.ts`
5. снова пересоберите UI:

```bash
pnpm -C /root/openclaw ui:build
```

---

## 💡 Рекомендация

Перед правками лучше сделать backup:

```bash
cp /root/openclaw/ui/src/i18n/lib/types.ts /root/openclaw/ui/src/i18n/lib/types.ts.bak
cp /root/openclaw/ui/src/i18n/lib/registry.ts /root/openclaw/ui/src/i18n/lib/registry.ts.bak
cp /root/openclaw/ui/src/i18n/locales/en.ts /root/openclaw/ui/src/i18n/locales/en.ts.bak
```

---

## 🤝 Для сообщества

Если хотите улучшить перевод:
- переводите глубже весь UI
- вычищайте оставшиеся английские хвосты
- делайте pull request / форк

Если сделаете полную русификацию без огрызков — вообще красавчики.

---

## 🛠 Авторство

Русификация подготовлена как практический community patch для OpenClaw Control UI.

Если пригодилось — используйте, допиливайте и не превращайте интерфейс в лингвистический колхоз 😄
