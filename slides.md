---
theme: default
highlighter: shiki
fonts:
  sans: Roboto
  serif: Roboto Slab
  mono: Fira Code
---

# Viper и Cleanenv для конфигурирования структур vs Велосипед
 
### Аносов Костя

<a href="https://github.com/goreflect/gostructor" target="_blank" alt="GitHub"
  class="abs-br m-6 text-xl icon-btn opacity-50 !border-none !hover:text-white">
  <carbon-logo-github />
</a>

<style>
.logo_kontur {
  width: 30;
  height: 30;
  margin-bottom:  60px;
  margin-left:auto;
}
</style>

<!--
Всем привет! Сегодня я буду рассказывать про конфигурацию и как я решал проблемы конфигурирования в своём проекте
-->
---

# Предистория

## Проект - 36 микросервисов и сервисов
## Стек: Python, Golang, Kotlin

## История началась до Контура
---

# Глоссарий

## Конфигурация - настройки
## Точечная конфигурация - конфигурация каждого отдельного поля
## Источник конфигурации - ресурс, откуда можно забрать данные

---

# Какие бывают источники

## Файловые (hocon, toml, yaml, ini, json)
## Кодовые
## Секреты (vault)
## Серверные (spring cloud config server)

---

# Главная боль

# Стейджинги