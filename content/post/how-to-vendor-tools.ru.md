---
title: "Как завендорить инструменты в Golang"
date: 2025-01-24T14:18:19+03:00
tags: ["golang", "tools", "vendoring"]
---

В Golang используются два подхода работы c зависимостями проекта:
использовать зависимости из общего кеша модулей или из папки `vendor` проекта.
В первом варианте полагаемся на то, что зависимости будут доступны по сети.
Во втором варианте нужные для сборки проекта зависимости помещены внутрь проекта.

В случае библиотек сначала обновляется список используемых зависимостей в `go.mod`, а затем из этих зависимостей формируется папка `vendor`.
Для этого выполните:

```sh
go mod tidy
go mod vendor
```

После выполнения этих двух команд в папке `vendor` будут скопированы все используемые библиотеки, а команды `go ...` будут искать зависимости в этой папке.
Причем вендорится только используемая часть кода.

Если в проекте используется `vendor`, естественными образом возникает желание подобным образом хранить еще и инструменты.
Например, `goimports` для форматирования импортов.
Этот процесс каверзный.
Для этого создаем файл `tools.go`. Можно в корне проекта, можно отдельным пакетом.

```go
//go:build tools
// +build tools

package tools

import (
    _ golang.org/x/tools/cmd/goimports
)
```

Начало файла - это [build constraint](https://pkg.go.dev/go/build#hdr-Build_Constraints) для сборки `tools`, по умолчанию этот файл не попадет в сборку.
`go mod tidy` будет работать с любым именем кроме `ignore`.

Имя пакета либо `main`, либо по имени директории.

Далее в секции `import` указываем пути к нужным инструментам.
Важно указать путь к `main` пакету инструмента, иначе в `vendor` будет не весь код.
При этом IDE буден сообщать об ошибке импорта пакета `main` - это ожидаемое.

Далее процесс аналогичен вендорингу библиотек:

```sh
go mod tidy
go mod vendor
```

В конце приятная новость.
В [Golang 1.24](https://tip.golang.org/doc/go1.24#go-command) в `go.mod` появится специальная директива `tools` для указания инструментов и этот трюк уйдет в прошлое.