---
theme: default
image: bg1.jpg
layout: image-left
highlighter: shiki
---

<img class="logo_kontur" src="logo-kontur.png" width="50"/> 

# Точечное конфигурирование полей структур из разных источников. Библиотека Gostructor
 
### Аносов Костя
### Разработчик из СКБ Контур


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

---

# Краткий план доклада

- Предистория
- Конфигурация глазами разработчика
- Популярные подходы, используемые go разработчиками
- Подход точечной конфигурации
- Приоритезация источников
- Библиотека Gostructor
  1. Поддержанные источники
  2. Поддержанные типы
  3. Бенчмарки
  4. Особенности парсинга структур
  5. Примеры использования


<style>
h1 {
  background-color: white;
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent; 
  -moz-text-fill-color: transparent;
}
</style>


---

# Предистория

<img src="slide-images/3/1.jpg" width="150">

<img src="slide-images/3/2.jpg" width="150">

---

# Конфигурация глазами разработчика


```go {all|1-5|7|8|9|10-14|11|all}
type ServiceConfiguration struct {
  URLDatabase string
  amountRetry int16
  loginAsAdmin uint8
}

func configure() Test {
  var source interface{}
  // здесь получение данных из какого-нибудь источника и преобразование к map[string]interface{}
  return Test {
    field1: source.get("field1").(string),
    field2: source.get("field2").(int16),
    field3: 1
  }
}
```

---

# Пример конфигурации

```yaml
database:
  connectionUri: "database connection uri"
  connectionPort: 27017
  username: test
  password: admin

  connect:
    maxWait: 15
    typeBalance: 2

server:
  port: 8080
  logging:
    enabled: true
    elasticSearch:
      enabled: true
      address: https://{elastic}.kubitre.me
```

---

# Описание модели конфигурации на go

```go
type (
  Configuration struct {
    Server ServerConfiguration
    Database DatabaseConfiguration
  }

  DatabaseConfiguration struct {
    ConnectionUri string
    ConnectionPort int16
    Username string
    Password string
    Connect ConnectConfiguration
  }

  ConnectConfiguration struct {
    MaxWait int32
    TypeBalance uint8
  }

  ServerConfiguration struct {
    Port int32
    Logging Bool
  }
)

```

---


# Ручной подход

```go
func parseYaml(fileName string) Parser {
  file, err := ioutil.ReadFile(fileName)
  ///здесь обработка ошибки
  var model Configuration
  if err := yaml.Unmarshal(file, &model); err != nil {
    // обработка ошибки
  }
	return model
}

func main() {
  fileName := os.Args[1:][0]
  model := parseYaml(fileName)
  // и только здесь вы можете уже начинать писать бизнес код. И то, это только конфигурация из одного источника
}

```

---

# Viper

```go
func main() {
  viper.SetConfigName("config")
  viper.SetConfigType("yaml")
	viper.AddConfigPath(".")
	var configuration Configuration

	if err := viper.ReadInConfig(); err != nil {
		log.Fatalf("Error reading config file, %s", err)
	}
	err := viper.Unmarshal(&configuration)
	if err != nil {
		log.Fatalf("unable to decode into struct, %v", err)
	}
}
```

---

# Viper.Плюсы

# Viper.Плюсы

# Cleanenv


# Точечное конфигурирование

Модифицируем исходную модель 

```go
type (
  Configuration struct {
    Server ServerConfiguration
    Database DatabaseConfiguration
  }

  DatabaseConfiguration struct {
    ConnectionUri string `cf_env:"MONGO_URL" cf_default:"database"`
    ConnectionPort int16 `cf_hocon:"port" cf_env:"MONGO_PORT" cf_default:"27017"`
    Username string `cf_hocon:"user" cf_env:"MONGO_PASS"`
    Password string `cf_toml:"pwd" cf_env:"MONGO_PASS"`
    Connect ConnectConfiguration
  }

  ConnectConfiguration struct {
    MaxWait int32 `cf_env:"MAX_WAIT"`
    TypeBalance uint8 `cf_env:"TYPE" cf_default:"2"`
  }

  ServerConfiguration struct {
    Port int32 `cf_env:"SERVER_PORT" cf_default:"9999"`
    Logging Bool `cf_ini:"SERVER#logging"
  }
)

```

---


# Библиотека Gostructor

<iframe width="768" height="432" src="https://miro.com/app/live-embed/o9J_lFbzqCs=/?moveToViewport=-931,-954,2839,2877" frameBorder="0" scrolling="no" allowFullScreen></iframe>

---

# Конфигурация в коде

```go
func main() {
  var configuration Configuration
  _, errConfiguring := gostructor.ConfigureSmart(&configuration)
  // check errConfiguring for any errors
  if errConfiguring != nil {
      /// action for error
  }

  // здесь уже можно использовать сконфигурированную структуру
  
}
```

--- 

# Плюсы. Точечная конфигурация
 
```go
type TestConfig struct {
  field1 string `cf_env:"myValue" cf_default:"1234" cf_hocon:"test"`
  field2 int16 `cf_hocon:"test2" cf_default:"1"`
  field3 []string `cf_toml:"tururu" cf_default:"myValue1,myValue2"`
}
```

---

# Плюсы. Гибкая система источников

```go
package pipeline


import "github.com/goreflect/gostructor/infra"


// IConfigure - configurer interface for chain pipeline configuration
type IConfigure interface {
	GetComplexType(*structContext) infra.GoStructorValue
	GetBaseType(*structContext) infra.GoStructorValue
}
```

---

# Плюсы. Точечная приоритезация

```go
type TestConfig struct {
  field1 string `cf_env:"myValue" cf_default:"4321" cf_hocon:"test" cf_priority:"local:cf_hocon,cf_default;cloud:cf_env,cf_default;prod:cf_env"`
  field2 int16 `cf_hocon:"test2" cf_default:"1" cf_priority:"local:cf_default,prod:cf_hocon"`
}
```

---

# Плюсы. Обработка ошибок внутри

```go
type (
	GoStructorValue struct {
		Value     reflect.Value
		notAValue *NotAValue
	}

	NotAValue struct {
		ValueAddress interface{}
		Error        error
	}
)
```
 
---

# Минусы. Всё ещё мало источников

1. Файловые источники: <span class="supported">TOML</span>|<span class="supported">HOCON</span>|<span class="supported">INI</span>|<span class="supported">JSON</span>|<span class="supported">YAML\YML</span>|<span class="not_supported">PROPERTIES</span>
2. Серверные источники:
  1. <span class="not_supported">Key\Value (Consul\etcd)</span>
  2. <span class="supported">Spring Cloud Config Server</span>
  3. <span class="not_supported">Gostructor-server</span>
3. Системные:
  1. <span class="supported">Переменные окружения</span>
  2. <span class="supported">Значения по умолчанию</span>
  3. <span class="supported">Аргументы командной строки</span>
4. <span class="not_supported">Кастомный сеттер для полей</span>

<style>
.not_supported {
  color: red;
}
.supported {
  color: green;
}
</style>

---

# Минусы. Нет горячих настроек (Proposal 1.0)



---

# Минусы. Рефлексия

```go
unsafe.Pointer{}
relfect.Interface{}
```

#