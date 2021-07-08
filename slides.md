---
theme: default
layout: center
highlighter: shiki
fonts:
  sans: Roboto
  serif: Roboto Slab
  mono: Roboto
  weights: '400,800'
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

<style>
h2{
  padding-top: 55px;
}
</style>
---

# Предистория

## Проект - 36 микросервисов и сервисов
## Стек: Python, Golang, Kotlin

<style>
h2{
  padding-top: 55px;
}
</style>
---

# Предистория

## Проект - 36 микросервисов и сервисов
## Стек: Python, Golang, Kotlin

## История началась до Контура

<style>
h2{
  padding-top: 55px;
}
</style>
---

# Глоссарий

## Точечная конфигурация - конфигурация каждого отдельного поля

<style>
h2{
  padding-top: 55px;
}
</style>
---

# Глоссарий

## Точечная конфигурация - конфигурация каждого отдельного поля
## Источник конфигурации - ресурс, откуда можно забрать данные


<style>
h2{
  padding-top: 55px;
}
</style>
---

# Какие бывают источники

## Файловые (hocon, toml, yaml, ini, json)

<style>
h2{
  padding-top: 25px;
}
</style>

---

# Какие бывают источники

## Файловые (hocon, toml, yaml, ini, json)
## Кодовые(дефолтные значения)

<style>
h2{
  padding-top: 25px;
}
</style>

---

# Какие бывают источники

## Файловые (hocon, toml, yaml, ini, json)
## Кодовые (дефолтные значения)
## Секреты (vault)

<style>
h2{
  padding-top: 25px;
}
</style>

---

# Какие бывают источники

## Файловые (hocon, toml, yaml, ini, json)
## Кодовые (дефолтные значения)
## Секреты (vault)
## Серверные (spring cloud config server, key\value)

<style>
h2{
  padding-top: 25px;
}
</style>

---

# Главная боль - Стейджинги

<img src="/slide-images/11.png"/>
---

## Так а причём здесь го?


<style>
h2 {
  text-align: center;
  padding-top: auto;
}
</style>

---

# Dev 

<img src="/slide-images/12.png" height={40}/>


<style>
h1 {
  text-align: center;
  
}
</style>

---

# Test

<img src="/slide-images/13.png" height="30"/>


<style>
h1 {
  text-align: center;
  
}
</style>

---

# Prod

<img src="/slide-images/14.png" height="30"/>


<style>
h1 {
  text-align: center;
}
</style>

---

# Каковы ожидания от решения?

## 1. Конфигурирование сервисов данными из разных источников

<style>
h2 {
  padding-top: 25px;
}
</style>
---

# Каковы ожидания от решения?

## 1. Конфигурирование сервисов данными из разных источников
## 2. Точечная подстановка значений полям

<style>
h2 {
  padding-top: 25px;
}
</style>
---

# Каковы ожидания от решения?

## 1. Конфигурирование сервисов данными из разных источников
## 2. Точечная подстановка значений полям
## 3. Как можно больше требуемых источников

<style>
h2 {
  padding-top: 25px;
}
</style>
---

# Критерии отбора решения

## 1. Возможность точечной конфигурации

<style>
h2{
  padding-top: 25px;
}
</style>

---

# Критерии отбора решения

## 1. Возможность точечной конфигурации
## 2. Должны поддерживаться источники (vault, hocon, default, env, spring config server)
<style>
h2{
  padding-top: 25px;
}
</style>

---

# Критерии отбора решения

## 1. Возможность точечной конфигурации
## 2. Должны поддерживаться источники (vault, hocon, default, env, spring config server)
## 3. Понятная структура ошибок

<style>
h2{
  padding-top: 25px;
}
</style>

---

# Критерии отбора решения

## 1. Возможность точечной конфигурации
## 2. Должны поддерживаться источники (vault, hocon, default, env, spring config server)
## 3. Понятная структура ошибок
## 4. Небольшой объём написания инфраструктурного кода

<style>
h2{
  padding-top: 25px;
}
</style>

---

# Ручной подход


```go
type ServiceConfiguration struct {
	Main           MainConfig
	Db             DatabaseConfig
	ServiceA       IntegrationСonf
	BusinessSecret BusinessConf 
}
```
<style>
code {
  font-size: 2.7em;
  line-height: 1.5;
}
</style>
---

# Ручной подход


```go
type MainConfig struct {
	IsKubernetes    bool
	ServiceName     string
	StrategyRequest string
}
```

<style>
code {
  font-size: 3.3em;
  line-height: 1.5;
}
</style>
---

# Ручной подход


```go
type DatabaseConfig struct {
	Replicas []string
	Username string
	Password string
}
```

<style>
code {
  font-size: 3.3em;
  line-height: 1.5;
}
</style>
---


# Ручной подход


```go
type IntegrationConf struct {
	ApiKey          string
	StrategyRequest string
	RateLimit       int16
}
```

<style>
code {
  font-size: 3.3em;
  line-height: 1.5;
}
</style>
---

# Ручной подход


```go
type BusinessConf struct {
	PrivateKeyPath  string
	PrivateCertPath string
}
```

<style>
code {
  font-size: 3.3em;
  line-height: 1.5;
}
</style>
---

# Рассмотрим конфигурацию для Dev стейджинга

## В качестве источников используем **json** и **дефолтные значения**

<style>
h2{
  padding-top: 50px
}
</style>