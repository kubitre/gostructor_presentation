---
theme: default
layout: center
highlighter: shiki
fonts:
  sans: Roboto
  serif: Roboto Slab
  mono: Roboto
  weights: '400,800'
download: true
---

# Viper и Cleanenv для конфигурирования структур vs Велосипед
 
### Аносов Костя


<div class="logo_github">
  <img class="logo_kontur" src="https://goreflect.github.io/slide-images/kontur.png"/>

  <a href="https://github.com/goreflect/gostructor" target="_blank" alt="GitHub"
    class="abs-br m-6 text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

<style>

h3 {
  position: absolute;
  right: 25px;
  font-size: 1em;

}

.logo_kontur {
  height: 30px;
  margin-right:auto;
  position: fixed;
  bottom: 20px;
}
</style>

<!--
Всем привет! Сегодня я буду рассказывать про конфигурацию и как я решал проблемы конфигурирования в своём проекте
-->

---

# Предистория

## История началась до Контура

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 55px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}
</style>
---

# Предистория

## История началась до Контура
## Проект - 36 микросервисов и сервисов

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 55px;
}

.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}
</style>
---

# Предистория

## История началась до Контура
## Проект - 36 микросервисов и сервисов
## Стек: Python, Golang, Kotlin


<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 55px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>
---

# Глоссарий

## ***Точечная конфигурация*** - конфигурация каждого отдельного поля
<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 55px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>
---

# Глоссарий

## ***Точечная конфигурация*** - конфигурация каждого отдельного поля
## ***Источник конфигурации*** - ресурс

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>


<style>
h2{
  padding-top: 55px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>
---

# Какие бывают источники

## 1. hocon, toml, yaml, ini, json

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Какие бывают источники

## 1. hocon, toml, yaml, ini, json
## 2. дефолтные значения, переменные окружения

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Какие бывают источники

## 1. hocon, toml, yaml, ini, json
## 2. дефолтные значения, переменные окружения
## 3. vault

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Какие бывают источники

## 1. hocon, toml, yaml, ini, json
## 2. дефолтные значения, переменные окружения
## 3. vault
## 4. config file server(spring cloud config server), key\value store(consul, etcd, firestore) 

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

## Так а причём здесь го?


<img src="https://goreflect.github.io/slide-images/go_bg_3.jpg" />

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2 {
  text-align: center;
  padding-top: auto;
}

img {
  
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Главная боль - Стейджинги

<img src="https://goreflect.github.io/slide-images/11.png"/>

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>

.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}
</style>
---

# Dev 

<img src="https://goreflect.github.io/slide-images/12.png" height={40}/>

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h1 {
  text-align: center;
  
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Test

<img src="https://goreflect.github.io/slide-images/13.png" height="30"/>

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h1 {
  text-align: center;
  
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Prod

<img src="https://goreflect.github.io/slide-images/14.png" height="30"/>

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h1 {
  text-align: center;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Критерии отбора решения

## 1. Есть ли точечная конфигурация?

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Критерии отбора решения

## 1. Есть ли точечная конфигурация?
## 2. vault, hocon, default, env, spring config server

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Критерии отбора решения

## 1. Есть ли точечная конфигурация?
## 2. vault, hocon, default, env, spring config server
## 3. Понятная структура ошибок

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Критерии отбора решения

## 1. Есть ли точечная конфигурация?
## 2. vault, hocon, default, env, spring config server
## 3. Понятная структура ошибок
## 4. Небольшой объём написания инфраструктурного кода

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Какие решения рассмотрю

<img src="https://goreflect.github.io/slide-images/infoGraphics/vs.png"/>

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>

img {
  height: 450px;
  margin-left: auto;
  margin-right: auto;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}
</style>

---

# Конфигурация окружения

<img src="https://goreflect.github.io/slide-images/infoGraphics/hand_env_config.png"/>

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
img {
  height: 500px;
  margin-left: auto;
  margin-right: auto;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Мапим значения из источников

<img src="https://goreflect.github.io/slide-images/infoGraphics/hand_config.png"/>

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
img {
  height: 450px;
  margin-left: auto;
  margin-right: auto;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Что будем конфигурировать?


```go{all|2}
type ServiceConfiguration struct {
	Main           MainConfig
	Db             DatabaseConfig
	ServiceA       IntegrationСonf
	BusinessSecret BusinessConf 
}
```

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 2.7em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
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

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 3.3em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Что будем конфигурировать?

```go{all|3}
type ServiceConfiguration struct {
	Main           MainConfig
	Db             DatabaseConfig
	ServiceA       IntegrationСonf
	BusinessSecret BusinessConf 
}
```

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 2.7em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
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

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 3.3em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>
---

# Что будем конфигурировать?

```go{all|4}
type ServiceConfiguration struct {
	Main           MainConfig
	Db             DatabaseConfig
	ServiceA       IntegrationСonf
	BusinessSecret BusinessConf 
}
```

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 2.7em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
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

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 3.3em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>
---

# Что будем конфигурировать?

```go{all|5}
type ServiceConfiguration struct {
	Main           MainConfig
	Db             DatabaseConfig
	ServiceA       IntegrationСonf
	BusinessSecret BusinessConf 
}
```

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 2.7em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
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

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 3.3em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Как будет выглядеть конфигурация окружения?

```yaml{all|2|7|9|11|13|3-5|8|10|all}
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

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 1.5em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Сконфигурируем

```go{all|4}
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

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 2em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Читаем настройки окружения

```go{all|3|8|all}
func readSourceConfig(file string) (
  map[string]interface{}, error) {
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

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 2em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Продолжим описывать ReadConfig

```go
func ReadConfig(configSources string) (
  ServiceConfiguration, 
  error) {
  // чтение конфигурации окружения
  var configuration ServiceConfiguration
  sources := configSource["sources"]
  .(map[interface{}]interface{}) 
  // продолжение на следующем слайде
}
```

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 2em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Разбираем источники

```go{all|3-5}
  for key, source := range sources {
		switch key {
		case "json":
          if err := configuration.addFile(source.(map[string]interface{})
            ["pathToFile"].(string)); err != nil {
            return ServiceConfiguration{}, err
		  }
    break
    ....
	}
```

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 1.5em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Метод для чтения и мержа с получателем конфигурации

```go{all|3}
func (config *ServiceConfiguration) addFile(file string) 
error {
	configurationByFile, err := readFile(file)
	if err != nil {
		return err
	}
	return mergo.MergeWithOverwrite(config, &configurationByFile)
}

```

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 2em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---


# Как будем читать конфигурацию из файлика

```go{all|2|7|all}
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

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 2em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Мержим с нашей конфигурацией

```go{7-8|all}
func (config *ServiceConfiguration) addFile(file string) 
error {
	configurationByFile, err := readFile(file)
	if err != nil {
		return err
	}
  return mergo.MergeWithOverwrite(config, 
    &configurationByFile)
}

```

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 2em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Идентично для оставшихся источников

```go{all|2|3}
  case "vault":
    if err := configuration.addVault(source
      .(map[interface{}]interface{})); err != nil {
      return ServiceConfiguration{}, err
    }
    break
```

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 2em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---


# Конфигурируем из волта

```go
func (config *ServiceConfiguration) addVault(
  dataFromEnv map[interface{}]interface{}) error {
	configurationVault := ConfigVault{
		VaultAddress: dataFromEnv["Address"].(string),
		VaultPath:    dataFromEnv["Path"].(string),
		VaultToken:   dataFromEnv["Token"].(string),
	}
  ...
}
```

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 2em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

#  Конфигурируем из волта

```go{all|2}
...
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
}
```

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 1.5em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Подключение к волту

```go{2-4|9|all}
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

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 1.5em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}
</style>
---

#  Конфигурируем из волта

```go{6}
...
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
}
```

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 1.5em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Получение данных из волта

```go{3|7|all}
func (cfg ConfigVault) getPath(path string) (
  map[string]interface{}, error) {
	pathSecrets, err := cfg.Connection.Logical().Read(path)
	if err != nil {
		return nil, err
	}
	return pathSecrets.Data, nil
}
```

<style>
code {
  font-size: 1.5em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

---

#  Конфигурируем из волта

```go{all|10-12}
...
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
}
```

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 1.5em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Для переменных окружения

```go{1-2}
  case "env":
    if err := configuration.addEnv(); err != nil {
      return ServiceConfiguration{}, err
    }
```

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 1.5em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>


---

# Опишем чтение из переменных окружения

```go{all|4|5|8|11|all}
func (config *ServiceConfiguration) addEnv() error {
	configurationByEnv := ServiceConfiguration{
		Main: MainConfig{
			ServiceName:     os.Getenv("SERVICE_NAME"),
			StrategyRequest: os.Getenv("STRATEGY_REQUEST"),
		},
		Db: DatabaseConfig{
			Replicas: strings.Split(os.Getenv("MONGO_REPLICAS"), ","),
		},
		ServiceA: IntegrationConf{
			StrategyRequest: os.Getenv("GOOGLE_AI_STRATEGY_REQUEST"),
		},
	}
	return mergo.MergeWithOverwrite(config, configurationByEnv)
}
```

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 1.5em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>


---

# Для значений по умолчанию

```go{all}
  case "default":
    configuration.addDefault()
  }
```

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 1.5em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>


---

# Дефолтные значения конфигурации

```go
func (config *ServiceConfiguration) addDefault() {
	config.Main.StrategyRequest = "Sequential"
	config.ServiceA.StrategyRequest = "Sequential"
}
```

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 2.3em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>


---

# Удовлетворило ли такое решение?

## 1. 167 строк кода

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>


---

# Удовлетворило ли такое решение?

## 1. 167 строк кода
## 2. Точечной конфигурации нет

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>


---

# Удовлетворило ли такое решение?

## 1. 167 строк кода
## 2. Точечной конфигурации нет
## 3. Дополнительный код

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>


---

# Viper

<img class="logo" src="https://goreflect.github.io/slide-images/viper.png" height="30"/>
<img class="social" src="https://goreflect.github.io/slide-images/viper_social.png"/>

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
.qr {
  height: 350px;
  margin-left: auto;
  margin-right: auto;
}
.logo {
  height: 100px;
  margin-left: auto;
  margin-right: auto;
}

.social{
  height: 50px;
  margin-left: auto;
  margin-right: auto;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Viper

<img class="logo" src="https://goreflect.github.io/slide-images/viper.png" height="30"/>
<img class="social" src="https://goreflect.github.io/slide-images/viper_social.png"/>

#### Ссылка на гитхаб: https://github.com/spf13/viper

<img class="qr" src="https://goreflect.github.io/slide-images/viper_github.png" height="50"/>

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h4 {
  text-align: center;
}
.qr {
  height: 300px;
  margin-left: auto;
  margin-right: auto;
}
.logo {
  height: 100px;
  margin-left: auto;
  margin-right: auto;
}

.social{
  height: 50px;
  margin-left: auto;
  margin-right: auto;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# 1 Шаг настройка

<img src="https://goreflect.github.io/slide-images/infoGraphics/viper_settings.png"/>

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
img {
  height: 450px;
  margin-left: auto;
  margin-right: auto;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# 2 Шаг получение значений

<img src="https://goreflect.github.io/slide-images/infoGraphics/viper_get_values.png"/>

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
img {
  height: 450px;
  margin-left: auto;
  margin-right: auto;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Сконфигурируем viper

```go{all|3|5,6,8,10|7,9|all}
func settingViper() {
	viper.SetConfigName("ServiceConfiguration")
	viper.SetConfigType("json")
	viper.AddConfigPath(".")
	viper.BindEnv("service_name", "Main.ServiceName")
	viper.BindEnv("strategy_request", "Main.StrategyRequest")
	viper.SetDefault("Main.StrategyRequest", "Sequential")
	viper.BindEnv("google_ai_strategy_request", "ServiceA.StrategyRequest")
	viper.SetDefault("ServiceA.StrategyRequest", "Sequential")
	viper.BindEnv("mongo_replicas", "Db.Replicas")
}
```

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 1.6em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>


---

# Опишем функционал по чтению конфигурации 

```go{all|2-6}
func ReadConfig(path string) (ServiceConfiguration, error) {
	sourceConfig := readSourceConfig(path)
	var configuration ServiceConfiguration
	if err := viper.Unmarshal(&configuration); err != nil {
		return ServiceConfiguration{}, err
	}
	for key, _ := range data {
		switch key {
		case "vault":
			if err := configuration.addVault(configurationSource.GetStringMap("source.vault")); err != nil {
				return ServiceConfiguration{}, err
			}
		}
	}
	return configuration, nil
}
```

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 1.5em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>


---

# Прочтём конфигурацию окружения

```go
func readSourceConfig(fileName string)(map[string]interface{}) {
  configurationSource := viper.New()
	configurationSource.AddConfigPath(".")
	configurationSource.SetConfigFile(fileName)
	data := configurationSource.GetStringMap("sources")
}
```

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 1.8em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>


---

# Описываем функциона по чтению конфигурации

```go{4|9-10}
func ReadConfig(path string) (ServiceConfiguration, error) {
	sourceConfig := readSourceConfig(path)
	var configuration ServiceConfiguration
	if err := viper.Unmarshal(&configuration); err != nil {
		return ServiceConfiguration{}, err
	}
	for key, _ := range data {
		switch key {
		case "vault":
			if err := configuration.addVault(configurationSource.GetStringMap("source.vault")); err != nil {
				return ServiceConfiguration{}, err
			}
		}
	}
	return configuration, nil
}
```

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 1.8em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>


---

# Чтение из Vault

```go{all}
func (config *ServiceConfiguration) addVault(dataFromEnv 
map[interface{}]interface{}) error {
	configurationVault := ConfigVault{
		VaultAddress: dataFromEnv["Address"].(string),
		VaultPath:    dataFromEnv["Path"].(string),
		VaultToken:   dataFromEnv["Token"].(string),
  }
  
  if err := configurationVault.connectToVault(); err != nil {
		return err
	}

  configFromVaultDatabase, err := vaultConfig
    .getPath(configurationVault.VaultPath)
	if err != nil {
		return err
	}
	config.BusinessSecret.PrivateCertPath = configFromVaultDatabase["certPath"].(string)
	config.BusinessSecret.PrivateKeyPath = configFromVaultDatabase["keyPath"].(string)
	config.ServiceA.ApiKey = configFromVaultDatabase["ApiKey"].(string)
	return nil
```

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 1.1em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Теперь к метрикам

## 1. 113 строчек кода

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>
---


# Теперь к метрикам

## 1. 113 строчек кода
## 2. Точечной конфигурации нет

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Теперь к метрикам

## 1. 113 строчек кода
## 2. Точечной конфигурации нет
## 3. Дополнительный инфровый код

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Теперь к метрикам

## 1. 113 строчек кода
## 2. Точечной конфигурация +-
## 3. Дополнительный инфровый код
## 4. Фиксированный порядок источников

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Cleanenv

<img class="logo" src="https://goreflect.github.io/slide-images/cleanenv_logo.png" height="30"/>
<img class="social" src="https://goreflect.github.io/slide-images/cleanenv_social.png"/>

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>

.qr {
  height: 250px;
  margin-left: auto;
  margin-right: auto;
}
.logo {
  height: 100px;
  margin-left: auto;
  margin-right: auto;
}

.social{
  height: 50px;
  margin-left: auto;
  margin-right: auto;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Cleanenv

<img class="logo" src="https://goreflect.github.io/slide-images/cleanenv_logo.png" height="30"/>
<img class="social" src="https://goreflect.github.io/slide-images/cleanenv_social.png"/>

#### Ссылка на гитхаб: https://github.com/ilyakaznacheev/cleanenv

<img class="qr" src="https://goreflect.github.io/slide-images/cleanenv_github.png" height="50"/>

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h4 {
  text-align: center;
}
.qr {
  height: 250px;
  margin-left: auto;
  margin-right: auto;
}
.logo {
  height: 100px;
  margin-left: auto;
  margin-right: auto;
}

.social{
  height: 50px;
  margin-left: auto;
  margin-right: auto;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Теги в Go

<img src="https://goreflect.github.io/slide-images/infoGraphics/tags_go.png"/>

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
img {
  margin-left: auto;
  margin-right: auto;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Получение мета информации из тегов

<img src="https://goreflect.github.io/slide-images/infoGraphics/cleanenv_meta.png"/>

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
img {
  margin-left: auto;
  margin-right: auto;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Получение значений в порядке указания тегов

<img src="https://goreflect.github.io/slide-images/infoGraphics/cleanenv_config_struct.png"/>

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
img {
  margin-left: auto;
  margin-right: auto;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Используем следующие теги из этой библиотеки

## 1. env

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>
---


# Используем следующие теги из этой библиотеки

## 1. env
## 2. env-default

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>
---

# Модифицируем наши конфиг-структуры

```go{all|2|3|4-5|all}
type MainConfig struct {
	IsKubernetes    bool   `env-default:"true"`
	ServiceName     string `env:"SERVICE_NAME"`
    StrategyRequest string `env:"MAIN_STRATEGY_REQUEST" 
      env-default:"sequential"`
}
```

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 1.5em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Модифицируем конфиг-структуры

```go
type DatabaseConfig struct {
	Replicass []string `env:"MONGO_REPLICAS"`
	Username  string `json:"username"`
	Password  string `json:"password"`
}
```

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 1.5em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Модифицируем конфиг-структуры

```go
type IntegrationConf struct {
	ApiKey          string
	StrategyRequest string `env:"GOOGLE_AI_STRATEGY_REQUEST" env-default:"sequential"`
	RateLimit       int16
}
```

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 1.5em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Как будем читать конфигурацию

```go{all|2}
func ReadConfig(configSources string) (ServiceConfiguration, error) {
	configSource, err := readSourceConfig(configSources)
	if err != nil {
		return ServiceConfiguration{}, err
	}
	var configuration ServiceConfiguration
  sources := configSource["sources"].(map[interface{}]interface{})

  if err := cleanenv.ReadConfig(file, configuration); err != nil {
		return ServiceConfiguration{}, err
  }
  
	for key, source := range sources {
		switch key {
		case "vault":
			if err := configuration.addVault(source.(map[interface{}]interface{})); err != nil {
				return ServiceConfiguration{}, err
			}
		}
  }
	return configuration, nil
}


```

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 1.2em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Читаем настройки окружения

```go{all|3|8|all}
func readSourceConfig(file string) (
  map[string]interface{}, error) {
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

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 2em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Читаем конфигу

```go{6|7|9|15}
func ReadConfig(configSources string) (ServiceConfiguration, error) {
	configSource, err := readSourceConfig(configSources)
	if err != nil {
		return ServiceConfiguration{}, err
	}
	var configuration ServiceConfiguration
  sources := configSource["sources"].(map[interface{}]interface{})

  if err := cleanenv.ReadConfig(file, configuration); err != nil {
		return ServiceConfiguration{}, err
  }
  
	for key, source := range sources {
		switch key {
		case "vault":
			if err := configuration.addVault(source.(map[interface{}]interface{})); err != nil {
				return ServiceConfiguration{}, err
			}
		}
  }
	return configuration, nil
}


```

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 1.2em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Инфра для волта та же

```go

func (config *ServiceConfiguration) addVault(dataFromEnv map[interface{}]interface{}) error {
	configurationVault := ConfigVault{
		VaultAddress: dataFromEnv["Address"].(string),
		VaultPath:    dataFromEnv["Path"].(string),
		VaultToken:   dataFromEnv["Token"].(string),
	}

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
}
```

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}
</style>
---

# Метрики

## 1. 94 строчки кода

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Метрики

## 1. 94 строчки кода
## 2. Точечная конфигурация есть

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---


# Метрики

## 1. 94 строчки кода
## 2. Точечная конфигурация есть
## 3. Мало источников

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Метрики

## 1. 94 строчки кода
## 2. Точечная конфигурация есть
## 3. Мало источников
## 4. Порядок конфигурации жёстко зафиксирован

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Библиотека Gostructor

<img class="social" src="https://goreflect.github.io/slide-images/gostructor_social.png"/>

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<img src="https://goreflect.github.io/slide-images/LogotypeGostructor.png"/>

<style>
img {
  margin-top: 15px;
  height: 250px;
  margin-left: auto;
  margin-right: auto;
}
.qr {
  height: 250px;
  margin-left: auto;
  margin-right: auto;
}
.logo {
  height: 100px;
  margin-left: auto;
  margin-right: auto;
}

.social{
  height: 50px;
  margin-left: auto;
  margin-right: auto;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Библиотека Gostructor

<img class="social" src="https://goreflect.github.io/slide-images/gostructor_social.png"/>

Ссылка на гитхаб: https://github.com/goreflect/gostructor

<img class="qr" src="https://goreflect.github.io/slide-images/gostructor_github.png" height="50"/>

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
.qr {
  height: 250px;
  margin-left: auto;
  margin-right: auto;
}
.logo {
  height: 100px;
  margin-left: auto;
  margin-right: auto;
}

.social{
  height: 50px;
  margin-left: auto;
  margin-right: auto;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Получаем мета информацию из тегов

<img src="https://goreflect.github.io/slide-images/infoGraphics/gostructor_meta.png"/>

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
img {
  margin-left: auto;
  margin-right: auto;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Получаем значения

<img src="https://goreflect.github.io/slide-images/infoGraphics/gostructor_get_configs.png"/>

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
img {
  height: 450px;
  margin-left: auto;
  margin-right: auto;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Как выглядит мета информация в тегах

<img src="https://goreflect.github.io/slide-images/infoGraphics/gostructor_tag1.png"/>

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
img {
  height: 450px;
  margin-left: auto;
  margin-right: auto;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Приоритезация источников

<img src="https://goreflect.github.io/slide-images/infoGraphics/gostructor_priority_1.png"/>

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
img {
  height: 450px;
  margin-left: auto;
  margin-right: auto;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Кастомизация приоритетов в зависимости от окружения

<img src="https://goreflect.github.io/slide-images/infoGraphics/gostructor_priority2.png"/>

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
img {
  height: 450px;
  margin-left: auto;
  margin-right: auto;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Модифицируем наши структуры

```go
type MainConfig struct {
  IsKubernetes    bool   `cf_env:"KUBERNETES" 
    cf_default:"false"`
  ServiceName     string `cf_json:"name" 
    cf_env:"SERVICE_NAME" cf_default:"test"`
  StrategyRequest string `cf_default:"sequential"`
}
```

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 2em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Модифицируем наши структуры

```go{4-5|all}
type DatabaseConfig struct {
  Replicas []string `cf_env:"MONGO_REPLICAS"
    cf_default:"localhost:27017"`
  Username string   `cf_vault:"infra/mongo#username"`
  Password string   `cf_vault:"infra/mongo#password"`
}
```

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 2em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Модифицируем наши структуры

```go
type IntegrationConf struct {
  APIKey          string `cf_vault:"integration/serviceA#api-key" 
    cf_env:"SERVICE_A_KEY" cf_default:"testApi"`
  StrategyRequest string `cf_default:"sequential"`
  RateLimit       int16  `cf_default:"100"`
}
```

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 2em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Кастомизируем последовательность источников

```go{2|3}
type IntegrationConf struct {
  APIKey string `... cf_priority:"SEQUENCE_1:cf_env,
    cf_default;SEQUENCE_2:cf_vault"`
  ...
}
```

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 2em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Модифицируем наши структуры

```go
type BusinessConf struct {
  PrivateKeyPath  string `cf_vault:"services/
    businessService1#keyPath" cf_default:"/var/test.pem"`
  PrivateCertPath string `cf_vault:"services/
    businessService1#certPath" cf_default:"/var/test.crt"`
}
```

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 2em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Кастомизируем последовательность источников


```go{2,4|3,5}
type BusinessConf struct {
  PrivateKeyPath  string `cf_priority:"SEQUENCE_1:cf_default;
    SEQUENCE_2:cf_vault"`
  PrivateCertPath string `cf_priority:"SEQUENCE_1:cf_default;
    SEQUENCE_2:cf_vault"`
}
```

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 2em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---


# Как будем прокидывать настройку окружения? 

## Добавим в переменные окружения PRIORITY

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2 {
  font-size: 1.5em;
  margin-left: auto;
  margin-right: auto;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Читаем конфигурацию

```go{2|3|all}
func ReadConfig() (ServiceConfiguration, error) {
	var configuration ServiceConfiguration
	_, err := gostructor.ConfigureSmart(&configuration)
	if err != nil {
		return ServiceConfiguration{}, err
	}
	return configuration, nil
}

```

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
code {
  font-size: 2em;
  line-height: 1.5;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Плюсы gostructor

## 1. Автоматизация вне зависимости от окружения

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Плюсы gostructor

## 1. Автоматизация вне зависимости от окружения
## 2. Точечная конфигурация


<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Плюсы gostructor

## 1. Автоматизация вне зависимости от окружения
## 2. Точечная конфигурация
## 3. Множество источников


<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Плюсы gostructor

## 1. Автоматизация вне зависимости от окружения
## 2. Точечная конфигурация
## 3. Множество источников
## 4. Понятная система ошибок

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Минусы

## 1. Дополнительная зависимость + транзитивные зависимости в проект

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>


<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Минусы

## 1. Дополнительная зависимость + транзитивные зависимости в проект
## 2. Нет горячих настроек

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>


<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Минусы

## 1. Дополнительная зависимость + транзитивные зависимости в проект
## 2. Нет горячих настроек
## 3. Не поддержан Spring Cloud Config Server, key\value


<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Минусы

## 1. Дополнительная зависимость + транзитивные зависимости в проект
## 2. Нет горячих настроек
## 3. Не поддержан Spring Cloud Config Server, key\value
## 4. Небольшая популярность

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# В каких проектах я использовал gostructor

## 1. Skillmap

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# В каких проектах я использовал gostructor

## 1. Skillmap
## 2. AuthEvent

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# В каких проектах я использовал gostructor

## 1. Skillmap
## 2. AuthEvent
## 3. ECCM компании Eltex 

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Какие планы на библиотеку

## 1. Spring cloud config server

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Какие планы на библиотеку

## 1. Spring cloud config server
## 2. Key\Value (Consul & etcd)

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>


<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Какие планы на библиотеку

## 1. Spring cloud config server
## 2. Key\Value (Consul & etcd)
## 3. Упрощение синтаксиса в тегах

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>


<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Какие планы на библиотеку

## 1. Spring cloud config server
## 2. Key\Value (Consul & etcd)
## 3. Упрощение синтаксиса в тегах
## 4. Краткая документашка по полям 

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>


<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Какие планы на библиотеку

## 1. Spring cloud config server
## 2. Key\Value (Consul & etcd)
## 3. Упрощение синтаксиса в тегах
## 4. Краткая документашка по полям 
## 5. Отслеживание измнений в файлах

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Какие планы на библиотеку

## 1. Spring cloud config server
## 2. Key\Value (Consul & etcd)
## 3. Упрощение синтаксиса в тегах
## 4. Краткая документашка по полям 
## 5. Отслеживание измнений в файлах
## ...

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---


# Кому может подойти

## 1. Больше 1 стейджинга


<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---

# Кому может подойти

## 1. Больше 1 стейджинга
## 2. Больше 1 источника конфигурации

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---


# Кому может подойти

## 1. Больше 1 стейджинга
## 2. Больше 1 источника конфигурации
## 3. Кто не хочет писать лишний код

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---


# Кому может подойти

## 1. Больше 1 стейджинга
## 2. Больше 1 источника конфигурации
## 3. Кто не хочет писать лишний код
## 4. У кого конфигурация - строгий контракт

<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>
h2{
  padding-top: 25px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>

---


<img src="https://goreflect.github.io/slide-images/mems/end_mem.jpg"/>
<div class="number_slide">{{ $slidev.nav.currentPage.value }}</div>

<style>

img {
  margin-left: auto;
  margin-right: auto;
  height: 350px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}
</style>

---

# Спасибо за внимание

## Остались вопросы?

Ссылки: https://goreflect.github.io/links.txt

<img src="https://goreflect.github.io/slide-images/links.png"/>

<img class="logo_kontur" src="https://goreflect.github.io/slide-images/kontur.png"/>

<style>

img {
  height: 350px;
  margin-left: auto;
  margin-right: auto;
}
.logo_kontur {
  height: 30px;
  margin-right:auto;
  position: fixed;
  bottom: 20px;
}
.number_slide {
  position: absolute;
  bottom: 15px;
  right: 25px;
}

</style>
