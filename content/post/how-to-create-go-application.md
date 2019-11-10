+++
tags = ["golang", "programing", "howto"]
highlight = true
math = false
date = "2017-02-14T20:31:13+03:00"
title = "Как удобно сделать каркас приложения для Golang"

[header]
  image = ""
  caption = "Как удобно сделать каркас приложения для Golang"

+++

Golang -- прекрасный язык программирования, который в последнее время все больше и больше помогает мне решать рабочие и исследовательские задачи.
На нем очень удобно писать небольшие утилиты, которые довольно быстро пишутся и легко поддерживаются.

В данном посте хочу поделится с вами интересным способом создания каркаса приложения для Golang, который встретился мне в [этой статье](https://hackernoon.com/most-imported-golang-packages-some-insights-fb12915a07#.y8nbz12gx).
При этом приложение будет структурировано, а так же уже из коробки иметь систему команд и флагов командной строки.
А также возможность читать их из файла конфигурации и переменных окружения.

Для начала надо установить пакет [Cobra](https://github.com/spf13/cobra):

```
go get -v github.com/spf13/cobra/cobra
```

Затем следует запустить простую команду для shell:

```
$ cobra init $GOPATH/src/<domain>/<user_name>/<project_name> -a "<author_name>"
```
или для cmd:
```
$ cobra init %GOPATH%\src\<domain>\<user_name>\<project_name> -a "<author_name>"
```
где 

* **\<domain\>** -- хостинг для хранения пакета (например, github.com);
* **\<user_name\>** -- ваш логин для хостинге (для меня например, djbelyak);
* **\<project_name\>** -- название вашего проекта (например, hello-cobra);
* **\<author_name\>** -- ваше имя, которое будет использовано для генерированной лицензии кода (для меня, например, Ivan Belyavtsev).


> Удостоверьтесь, что переменная окружения `PATH` содержит в себе `GOBIN`

В папке проекта появится файл `LICENSE`, который содержит уже сгенерированный текст лицензии на код, файл `main.go`, который содержит в себе основной запускаемый код, а также файл `cmd/root.go` в котором сгенерирован начальный код для работы приложения.

Проверим что у нас получилось:
```
$ go run $GOPATH/src/<domain>/<user_name>/<project_name>/main.go
A longer description that spans multiple lines and likely contains
examples and usage of using your application. For example:

Cobra is a CLI library for Go that empowers applications.
This application is a tool to generate the needed files
to quickly create a Cobra application.

$ go run $GOPATH/src/<domain>/<user_name>/<project_name>/main.go --config
Error: flag needs an argument: --config
Usage:

Flags:
      --config string   config file (default is $HOME/.geneticpainting.yaml)
  -t, --toggle          Help message for toggle

flag needs an argument: --config
exit status 4294967295
```

Как видно из лога команды у нас уже есть некоторая справка и возможность указать конфигурационный файл..
Справочные сообщения можно найти и поправить в файле `cmd/root.go`.


Теперь добавим новую команду \<command_name\> для нашего приложения:
```
$ cd $GOPATH/src/<domain>/<user_name>/<project_name>
$ cobra add <command_name>
```
В результате работы этой команды будет сгенерирован новый файл `cmd/<command_name>`.
Запустим приложение и проверим как будет работать новая команда
```
$ go run $GOPATH/src/github.com/djbelyak/geneticpainting/main.go <command_name>
<command_name> called
```

И последнее что мы рассмотрим в этом посте -- добавление флагов.
Добавим глобальный флаг **-v, --version**.
Для этого в файле `cmd/root.go` объявим глобальную переменную
```
var printVersion bool
```
В функции `init()` добавим персистентный булевый флаг
```
RootCmd.PersistentFlags().BoolVarP(&printVersion, "version", "v", false, "print version of application")
```
А также в конструкторе объекта `RootCmd` добавим поле `Run`
```
Run: func(cmd *cobra.Command, args []string) {
		if printVersion {
			fmt.Println("Version 1.0.0")
		}
	}
```

Запустим и проверим работу флага
```
$ go run $GOPATH/src/github.com/djbelyak/geneticpainting/main.go -v
Version 1.0.0
```

### Полезные ссылки по теме

1. [Репозиторий проекта cobra](https://github.com/spf13/cobra)
2. [Документация пакета cobra](https://godoc.org/github.com/spf13/cobra)

