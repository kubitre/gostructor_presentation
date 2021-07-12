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


<div class="logo_github">
  <img class="logo_kontur" src="kontur.png"/>

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
## Источник конфигурации - ресурс


<style>
h2{
  padding-top: 55px;
}
</style>
---

# Какие бывают источники

## 1. hocon, toml, yaml, ini, json

<style>
h2{
  padding-top: 25px;
}
</style>

---

# Какие бывают источники

## 1. hocon, toml, yaml, ini, json
## 2. дефолтные значения, переменные окружения

<style>
h2{
  padding-top: 25px;
}
</style>

---

# Какие бывают источники

## 1. hocon, toml, yaml, ini, json
## 2. дефолтные значения, переменные окружения
## 3. vault

<style>
h2{
  padding-top: 25px;
}
</style>

---

# Какие бывают источники

## 1. hocon, toml, yaml, ini, json
## 2. дефолтные значения, переменные окружения
## 3. vault
## 4. config file server(spring cloud config server), key\value store(consul, etcd, firestore) 

<style>
h2{
  padding-top: 25px;
}
</style>

---

## Так а причём здесь го?


<style>
h2 {
  text-align: center;
  padding-top: auto;
}
</style>

---

# Главная боль - Стейджинги

<img src="/slide-images/11.png"/>

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


```go{2}
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

# Суммирующая структура

```go{all|3}
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

# Суммирующая структура

```go{all|4}
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

# Суммирующая структура

```go{all|5}
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
<style>
code {
  font-size: 2em;
  line-height: 1.5;
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
  // чтение конфигурации окружения
  var configuration ServiceConfiguration
  sources := configSource["sources"]
  .(map[interface{}]interface{}) 
  // продолжение на следующем слайде
}
```

<style>
code {
  font-size: 2em;
  line-height: 1.5;
}
</style>

---

# Разбираем источники

```go{all|3|4}
  for key, source := range sources {
		switch key {
		case "json":
          if err := configuration.addFile(source.(map[string]interface{})["pathToFile"].(string)); err != nil {
            return ServiceConfiguration{}, err
		  }
    break
    ....
	}
```

<style>
code {
  font-size: 1.5em;
  line-height: 1.5;
}
</style>

---

# Метод для чтения и мержа нашей конфигурации

```go{all|2}
func (config *ServiceConfiguration) addFile(file string) 
error {
	configurationByFile, err := readFile(file)
	if err != nil {
		return err
	}
	return mergo.MergeWithOverwrite(config, &configurationByFile)
}

```

<style>
code {
  font-size: 2em;
  line-height: 1.5;
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

<style>
code {
  font-size: 2em;
  line-height: 1.5;
}
</style>

---

# Мержим с нашей конфигурацией

```go{all|7-8|all}
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

<style>
code {
  font-size: 2em;
  line-height: 1.5;
}
</style>

---

# Идентично для оставшихся источников

```go{all|2|3}
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
```


<style>
code {
  font-size: 2em;
  line-height: 1.5;
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

<style>
code {
  font-size: 2em;
  line-height: 1.5;
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
<style>
code {
  font-size: 1.5em;
  line-height: 1.5;
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

<style>
code {
  font-size: 1.5em;
  line-height: 1.5;
}
</style>

---

# Опишем таким образом процесс для всех источников

```go{all|7}
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

<style>
code {
  font-size: 1.5em;
  line-height: 1.5;
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

<style>
code {
  font-size: 1.5em;
  line-height: 1.5;
}
</style>


---

# Остались значение по умолчанию

```go{all|11|12}
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

<style>
code {
  font-size: 1.5em;
  line-height: 1.5;
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

<style>
code {
  font-size: 2.3em;
  line-height: 1.5;
}
</style>


---

# Удовлетворило ли такое решение?

## 1. 167 строк кода


<style>
h2{
  padding-top: 25px;
}
</style>


---

# Удовлетворило ли такое решение?

## 1. 167 строк кода
## 2. Точечной конфигурации нет


<style>
h2{
  padding-top: 25px;
}
</style>


---

# Удовлетворило ли такое решение?

## 1. 167 строк кода
## 2. Точечной конфигурации нет
## 3. Дополнительный код


<style>
h2{
  padding-top: 25px;
}
</style>


---

<img class="logo" src="/slide-images/viper.png" height="30"/>
<img class="social" src="/slide-images/viper_social.png"/>

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
</style>

---

<img class="logo" src="/slide-images/viper.png" height="30"/>
<img class="social" src="/slide-images/viper_social.png"/>

#### Ссылка на гитхаб: https://github.com/spf13/viper

<img class="qr" src="/slide-images/viper_github.png" height="50"/>

<style>
h4 {
  text-align: center;
}
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
</style>

---

# Сконфигурируем viper

```go{all|4|5|7|all}
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

<style>
code {
  font-size: 1.6em;
  line-height: 1.5;
}
</style>


---

# Опишем функционал по чтению конфигурации 

```go{all|2}
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

<style>
code {
  font-size: 1.5em;
  line-height: 1.5;
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

<style>
code {
  font-size: 1.8em;
  line-height: 1.5;
}
</style>


---

# Описываем функциона по чтению конфигурации

```go{4|9|10}
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

<style>
code {
  font-size: 1.8em;
  line-height: 1.5;
}
</style>


---

# Конфигурируем из волта

```go
func (config *ServiceConfiguration) addVault(dataFromEnv 
map[interface{}]interface{}) error {
	configurationVault := ConfigVault{
		VaultAddress: dataFromEnv["Address"].(string),
		VaultPath:    dataFromEnv["Path"].(string),
		VaultToken:   dataFromEnv["Token"].(string),
	}
  ...
}
```

<style>
code {
  font-size: 1.8em;
  line-height: 1.5;
}
</style>


---

# Чтение из Vault

```go{all}
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

<style>
code {
  font-size: 1.5em;
  line-height: 1.5;
}
</style>


---

# Теперь к метрикам

## 1. 113 строчек кода


<style>
h2{
  padding-top: 25px;
}
</style>
---


# Теперь к метрикам

## 1. 113 строчек кода
## 2. Точечной конфигурации нет


<style>
h2{
  padding-top: 25px;
}
</style>

---

# Теперь к метрикам

## 1. 113 строчек кода
## 2. Точечной конфигурации нет
## 3. Дополнительный инфровый код


<style>
h2{
  padding-top: 25px;
}
</style>

---

# Теперь к метрикам

## 1. 113 строчек кода
## 2. Точечной конфигурации нет
## 3. Дополнительный инфровый код
## 4. Внутри касты типов без обработки ошибок



<style>
h2{
  padding-top: 25px;
}
</style>

---

# Cleanenv

<img class="logo" src="/slide-images/cleanenv_logo.png" height="30"/>
<img class="social" src="/slide-images/cleanenv_social.png"/>

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
</style>

---

# Cleanenv

<img class="logo" src="/slide-images/cleanenv_logo.png" height="30"/>
<img class="social" src="/slide-images/cleanenv_social.png"/>

#### Ссылка на гитхаб: https://github.com/ilyakaznacheev/cleanenv

<img class="qr" src="/slide-images/cleanenv_github.png" height="50"/>

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
</style>

---

# Модифицируем конфиг-структуры

```go{all|2|3|all}
type MainConfig struct {
	IsKubernetes    bool   `env-default:"true"`
	ServiceName     string `env:"SERVICE_NAME"`
	StrategyRequest string `env:"MAIN_STRATEGY_REQUEST" env-default:"sequential"`
}
```

<style>
code {
  font-size: 1.5em;
  line-height: 1.5;
}
</style>

---

# Модифицируем конфиг-структуры

```go
type DatabaseConfig struct {
	Replicass []string `env:"MONGO_REPLICAS"`
	Username  string
	Password  string
}
```

<style>
code {
  font-size: 1.5em;
  line-height: 1.5;
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

<style>
code {
  font-size: 1.5em;
  line-height: 1.5;
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

<style>
code {
  font-size: 1.5em;
  line-height: 1.5;
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
<style>
code {
  font-size: 2em;
  line-height: 1.5;
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

---

# Метрики

## 1. 94 строчки кода


<style>
h2{
  padding-top: 25px;
}
</style>

---

# Метрики

## 1. 94 строчки кода
## 2. Точечная конфигурация есть

<style>
h2{
  padding-top: 25px;
}
</style>

---


# Метрики

## 1. 94 строчки кода
## 2. Точечная конфигурация есть
## 3. Мало источников


<style>
h2{
  padding-top: 25px;
}
</style>

---

# Библиотека Gostructor

<img class="social" src="/slide-images/github_social.png"/>

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
</style>

---

# Библиотека Gostructor

<img class="social" src="/slide-images/github_social.png"/>

Ссылка на гитхаб: https://github.com/goreflect/gostructor

<img class="qr" src="/slide-images/gostructor_github.png" height="50"/>

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
</style>

---

# Модифицируем наши структуры

```go
type MainConfig struct {
	IsKubernetes    bool   `cf_env:"KUBERNETES" cf_default:"false"`
	ServiceName     string `cf_json:"name" cf_env:"SERVICE_NAME" cf_default:"test"`
	StrategyRequest string `cf_default:"sequential"`
}
```

---

# Модифицируем наши структуры

```go
type DatabaseConfig struct {
	Replicas []string `cf_env:"MONGO_REPLICAS" cf_default:"localhost:27017"`
	Username string   `cf_vault:"infra/mongo#username"`
	Password string   `cf_vault:"infra/mongo#password"`
}
```

---

# Модифицируем наши структуры

```go
type IntegrationConf struct {
	APIKey          string `cf_vault:"integration/serviceA#api-key" cf_env:"SERVICE_A_KEY" cf_default:"testApi" cf_priority:"TEST:cf_env,cf_default;PROD:cf_vault"`
	StrategyRequest string `cf_default:"sequential"`
	RateLimit       int16  `cf_default:"100"`
}
```

---


# Модифицируем наши структуры

```go
type BusinessConf struct {
	PrivateKeyPath  string `cf_vault:"services/businessService1#keyPath" cf_default:"/var/test.pem" cf_priority:"TEST:cf_default;PROD:cf_vault"`
	PrivateCertPath string `cf_vault:"services/businessService1#certPath" cf_default:"/var/test.crt" cf_priority:"TEST:cf_default;PROD:cf_vault"`
}
```

---


# Как будем прокидывать настройку окружения? 

Теги наше всё!

---

# Читаем конфигурацию

```go
func ReadConfig() (ServiceConfiguration, error) {
	var configuration ServiceConfiguration
	_, err := gostructor.ConfigureSmart(&configuration)
	if err != nil {
		return ServiceConfiguration{}, nil
	}
	return configuration, nil
}

```

---


# Метрики

## 1. 8 строчек кода


<style>
h2{
  padding-top: 25px;
}
</style>
---

# Метрики

## 1. 8 строчек кода
## 2. Точечная конфигурация есть


<style>
h2{
  padding-top: 25px;
}
</style>
---

# Метрики

## 1. 8 строчек кода
## 2. Точечная конфигурация есть
## 3. Много источников


<style>
h2{
  padding-top: 25px;
}
</style>

---

# Метрики

## 1. 8 строчек кода
## 2. Точечная конфигурация есть
## 3. Много источников
## 4. Есть возможность настраивать окружение


<style>
h2{
  padding-top: 25px;
}
</style>

---

# Плюсы gostructor

## 1. Автоматизация вне зависимости от окружения



<style>
h2{
  padding-top: 25px;
}
</style>

---

# Плюсы gostructor

## 1. Автоматизация вне зависимости от окружения
## 2. Точечная конфигурация



<style>
h2{
  padding-top: 25px;
}
</style>

---

# Плюсы gostructor

## 1. Автоматизация вне зависимости от окружения
## 2. Точечная конфигурация
## 3. Множество источников



<style>
h2{
  padding-top: 25px;
}
</style>

---

# Плюсы gostructor

## 1. Автоматизация вне зависимости от окружения
## 2. Точечная конфигурация
## 3. Множество источников
## 4. Понятная система ошибок


<style>
h2{
  padding-top: 25px;
}
</style>

---

# Минусы

## 1. Дополнительная зависимость + транзитивные зависимости в проект



<style>
h2{
  padding-top: 25px;
}
</style>

---

# Минусы

## 1. Дополнительная зависимость + транзитивные зависимости в проект
## 2. Нет горячих настроек



<style>
h2{
  padding-top: 25px;
}
</style>

---

# Минусы

## 1. Дополнительная зависимость + транзитивные зависимости в проект
## 2. Нет горячих настроек
## 3. Не поддержан Spring Cloud Config Server, key\value



<style>
h2{
  padding-top: 25px;
}
</style>

---

# Минусы

## 1. Дополнительная зависимость + транзитивные зависимости в проект
## 2. Нет горячих настроек
## 3. Не поддержан Spring Cloud Config Server, key\value
## 4. Небольшая популярность


<style>
h2{
  padding-top: 25px;
}
</style>

---

# В каких проектах я использовал gostructor

## 1. Skillmap


<style>
h2{
  padding-top: 25px;
}
</style>

---

# В каких проектах я использовал gostructor

## 1. Skillmap
## 2. AuthEvent


<style>
h2{
  padding-top: 25px;
}
</style>

---

# В каких проектах я использовал gostructor

## 1. Skillmap
## 2. AuthEvent
## 3. ECCM компании Eltex 


<style>
h2{
  padding-top: 25px;
}
</style>

---

# Какие планы на библиотеку

## 1. Spring cloud config server


<style>
h2{
  padding-top: 25px;
}
</style>

---

# Какие планы на библиотеку

## 1. Spring cloud config server
## 2. Key\Value (Consul & etcd)



<style>
h2{
  padding-top: 25px;
}
</style>

---

# Какие планы на библиотеку

## 1. Spring cloud config server
## 2. Key\Value (Consul & etcd)
## 3. Упрощение синтаксиса в тегах



<style>
h2{
  padding-top: 25px;
}
</style>

---

# Какие планы на библиотеку

## 1. Spring cloud config server
## 2. Key\Value (Consul & etcd)
## 3. Упрощение синтаксиса в тегах
## 4. Краткая документашка по полям 



<style>
h2{
  padding-top: 25px;
}
</style>

---

# Какие планы на библиотеку

## 1. Spring cloud config server
## 2. Key\Value (Consul & etcd)
## 3. Упрощение синтаксиса в тегах
## 4. Краткая документашка по полям 
## 5. Отслеживание измнений в файлах


<style>
h2{
  padding-top: 25px;
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


<style>
h2{
  padding-top: 25px;
}
</style>

---

# Кому может подойти

## 1. Больше 1 стейджинга
## 2. Больше 1 источника конфигурации
## 3. Кто не хочет писать лишний код


<style>
h2{
  padding-top: 25px;
}
</style>

---

# Кому может подойти

## 1. Больше 1 стейджинга



<style>
h2{
  padding-top: 25px;
}
</style>

---

# Кому может подойти

## 1. Больше 1 стейджинга
## 2. Больше 1 источника конфигурации


<style>
h2{
  padding-top: 25px;
}
</style>

---

# Напоследок

"Лучший тот код, который не написан"

---

# Спасибо за внимание

Дайте обратную связь по библиотеке
Контрибьютьте!
