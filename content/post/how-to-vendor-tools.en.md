---
title: "How to Vendor Tools"
date: 2025-01-24T14:18:16+03:00
tags: ["golang", "tools", "vendoring"]
---


In Golang, there are two approaches to working with project dependencies:

1. Using dependencies from a shared cache of modules or from the project's `vendor` directory.
2. Assuming that dependencies will be available over the network.

In the second approach, the necessary dependencies for building the project are placed inside the project itself.

**Vendoring libraries**

When using libraries, you first update the list of used dependencies in `go.mod`, and then create a `vendor` directory from these dependencies by running:

```sh
go mod tidy
go mod vendor
```

After executing these two commands, all used libraries will be copied into the `vendor` directory, and Go commands like `go ...` will look for dependencies there.
Only the actually used part of the code is vendored.

**Vendoring tools**

If your project uses `vendor`, you might also want to store related tools in a similar way.
For example, `goimports` for formatting imports.

Unfortunately, this process is not straightforward.
To create a vendored toolset, create a file called `tools.go`.
You can place it at the root of your project or as a separate package.

Here's an example:

```go
//go:build tools
// +build tools

package tools

import (
    _ golang.org/x/tools/cmd/goimports
)
```

The beginning of the file is a [build constraint](https://pkg.go.dev/go/build#hdr-Build_Constraints) for building `tools`.
By default, this file will not be included in the build.
You can use `go mod tidy` to remove any files named `ignore`.

Next, specify the paths to the necessary tools in the `import` section.
Make sure to include the path to the main package of each tool.

Finally, run:

```
go mod tidy
go mod vendor
```

**Nice surprise**

In [Golang 1.24](https://tip.golang.org/doc/go1.24#go-command), there's a new directive called `tools` that can be used directly in `go.mod`. This makes it easier to specify tools and eliminates the need for this workaround.