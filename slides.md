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

## hocon, toml, yaml, ini, json

<style>
h2{
  padding-top: 25px;
}
</style>

---

# Какие бывают источники

## hocon, toml, yaml, ini, json
## дефолтные значения, переменные окружения

<style>
h2{
  padding-top: 25px;
}
</style>

---

# Какие бывают источники

## hocon, toml, yaml, ini, json
## дефолтные значения, переменные окружения
## vault

<style>
h2{
  padding-top: 25px;
}
</style>

---

# Какие бывают источники

## hocon, toml, yaml, ini, json
## дефолтные значения, переменные окружения
## vault
## config file server(spring cloud config server), key\value store(consul, etcd, firestore) 

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

## 1. Конфигурация может быть в разных источниках

<style>
h2 {
  padding-top: 25px;
}
</style>
---

# Каковы ожидания от решения?

## 1. Конфигурация может быть в разных источниках
## 2. Точечная подстановка значений полям

<style>
h2 {
  padding-top: 25px;
}
</style>
---

# Каковы ожидания от решения?

## 1. Конфигурация может быть в разных источниках
## 2. Точечная подстановка значений полям
## 3. Количества доступных источников достаточно

<style>
h2 {
  padding-top: 25px;
}
</style>
---

# Критерии отбора решения

## 1. Есть ли точечная конфигурация?

<style>
h2{
  padding-top: 25px;
}
</style>

---

# Критерии отбора решения

## 1. Есть ли точечная конфигурация?
## 2. vault, hocon, default, env, spring config server
<style>
h2{
  padding-top: 25px;
}
</style>

---

# Критерии отбора решения

## 1. Есть ли точечная конфигурация?
## 2. vault, hocon, default, env, spring config server
## 3. Понятная структура ошибок

<style>
h2{
  padding-top: 25px;
}
</style>

---

# Критерии отбора решения

## 1. Есть ли точечная конфигурация?
## 2. vault, hocon, default, env, spring config server
## 3. Понятная структура ошибок
## 4. Небольшой объём написания инфраструктурного кода

<style>
h2{
  padding-top: 25px;
}
</style>

---

# Что будем конфигурировать?


```go{all|2|3|4|5|all}
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

# Что будем конфигурировать?


```go{all|2|3|4|all}
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

# Что будем конфигурировать?


```go{all|2|3|4|all}
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


# Что будем конфигурировать?


```go{all|2|3|4|all}
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

# Что будем конфигурировать?


```go{all|2|3|all}
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

# Как будет выглядеть конфигурация в конкретном окружении?

```yaml{all|2|7|9|11|13|all}
sources:
  vault:
    Address: $VAULT_ADDRESS
    Token: $VAULT_TOKEN
    Path: $VAULT_PATH

  json: 
    pathFile: $PATH_TO_CONFIG
  hocon:
    pathFile: $PATH_TO_CONFIG
  env:

  default:
```

<style>
code {
  font-size: 1.5em;
  line-height: 1.5;
}
</style>

---

# А теперь посмотрим на код, который придётся написать руками

```go

func ReadConfig(configSources string) (
  ServiceConfiguration, 
  error) {
	configSource, err := readSourceConfig(configSources)
	if err != nil {
		return ServiceConfiguration{}, err
	}
	// на следующем слайде
}

```
<style>
code {
  font-size: 2em;
  line-height: 1.5;
}
</style>

---

# Продолжим описывать ReadConfig

```go
func ReadConfig(configSources string) (
  ServiceConfiguration, 
  error) {
  // на предыдущем слайде
  var configuration ServiceConfiguration
  sources := configSource["sources"]
  .(map[interface{}]interface{}) 
  // Продолжение на следующем слайде  
}
```

<style>
code {
  font-size: 2em;
  line-height: 1.5;
}
</style>

---

# До сих пор пишем руками

```go
  for key, source := range sources {
		switch key {
		case "json":
          if err := configuration.addFile(source.(map[string]interface{})["pathToFile"].(string)); err != nil {
            return ServiceConfiguration{}, err
		  }
		break
    // Продолжение на следующем слайде
	}
```

<style>
code {
  font-size: 1.5em;
  line-height: 1.5;
}
</style>

---


# Опишем таким образом процесс для всех источников

```go{all|1|2|3|6|7|8|10|11|all}
  case "vault":
    if err := configuration.addVault(source.(map[interface{}]interface{})); err != nil {
      return ServiceConfiguration{}, err
    }
    break
  case "env":
    if err := configuration.addEnv(); err != nil {
      return ServiceConfiguration{}, err
    }
  case "default":
    configuration.addDefault()
  }
```

---

# А теперь в детали. Читаем настройки окружения

```go{all|2|3|4|6|7|10|all}
func readSourceConfig(file string) (map[string]interface{}, error) {
	readBytes, errReading := ioutil.ReadFile(file)
	if errReading != nil {
		return nil, errReading
	}
	var result map[string]interface{}
	if err := yaml.Unmarshal(readBytes, &result); err != nil {
		return nil, err
	}
	return result, nil
}
```

---

# Как будем читать конфигурацию из файлика

```go{all|2|3|4|6|7|8|10|all}
func readFile(file string) (ServiceConfiguration, error) {
	readBytes, errReading := ioutil.ReadFile(file)
	if errReading != nil {
		return ServiceConfiguration{}, errReading
	}
	var data ServiceConfiguration
	errUnmarshaling := json.Unmarshal(readBytes, &data)
	if errUnmarshaling != nil {
		return ServiceConfiguration{}, errUnmarshaling
	}
	return data, nil
}

```
---


# Метод для чтения и мержа нашей конфигурации

```go{all|2|6|all}
func (config *ServiceConfiguration) addFile(file string) error {
	configurationByFile, err := readFile(file)
	if err != nil {
		return err
	}
	return mergo.MergeWithOverwrite(config, &configurationByFile)
}

```
---

# Как поступим в Vault?

```go
func (config *ServiceConfiguration) addVault(dataFromEnv map[interface{}]interface{}) error {
	configurationVault := ConfigVault{
		VaultAddress: dataFromEnv["Address"].(string),
		VaultPath:    dataFromEnv["Path"].(string),
		VaultToken:   dataFromEnv["Token"].(string),
	}

	// Продолжение на следующем слайде
}
```
---

# Чтение из Vault

```go{all|1}
  if err := configurationVault.connectToVault(); err != nil {
		return err
	}

	configFromVaultDatabase, err := vaultConfig.getPath(configurationVault.VaultPath)
	if err != nil {
		return err
	}
	config.BusinessSecret.PrivateCertPath = configFromVaultDatabase["certPath"].(string)
	config.BusinessSecret.PrivateKeyPath = configFromVaultDatabase["keyPath"].(string)
	config.ServiceA.ApiKey = configFromVaultDatabase["ApiKey"].(string)
	return nil
```


---
# Подключение к волту

```go
func (cfg *ConfigVault) connectToVault() error {
	conn, errConnection := vault.NewClient(cfg.VaultAddress,
		vault.WithCaPath(""),
		vault.WithAuthToken(cfg.VaultToken))
	if errConnection != nil {
		return errConnection
	}
	conn.SetToken(cfg.VaultToken)
	cfg.Connection = conn
	log.Println("Connection are initialized")
	return nil
}
```