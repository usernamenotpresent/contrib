---
id: fgprof
---

# Fgprof

![Release](https://img.shields.io/github/v/tag/gofiber/contrib?filter=fgprof*)
[![Discord](https://img.shields.io/discord/704680098577514527?style=flat&label=%F0%9F%92%AC%20discord&color=00ACD7)](https://gofiber.io/discord)
![Test](https://github.com/usernamenotpresent/contrib/workflows/Tests/badge.svg)
![Security](https://github.com/usernamenotpresent/contrib/workflows/Security/badge.svg)
![Linter](https://github.com/usernamenotpresent/contrib/workflows/Linter/badge.svg)

[fgprof](https://github.com/felixge/fgprof) support for Fiber.

**Note: Requires Go 1.19 and above**

## Install

This middleware supports Fiber v2.

Using fgprof to profiling your Fiber app.

```
go get -u github.com/gofiber/fiber/v2
go get -u github.com/usernamenotpresent/contrib/fgprof
```

## Config

| Property | Type                      | Description                                                                                                                                      | Default |
|----------|---------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|---------|
| Next     | `func(c *fiber.Ctx) bool` | A function to skip this middleware when returned `true`.                                                                                         | `nil`   |
| Prefix   | `string`.                 | Prefix defines a URL prefix added before "/debug/fgprof". Note that it should start with (but not end with) a slash. Example: "/federated-fiber" | `""`    |

## Example

```go
package main

import (
	"log"

	"github.com/usernamenotpresent/contrib/fgprof"
	"github.com/gofiber/fiber/v2"
)

func main() {
	app := fiber.New()
	app.Use(fgprof.New())
	app.Get("/", func(c *fiber.Ctx) error {
		return c.SendString("OK")
	})
	log.Fatal(app.Listen(":3000"))
}
```

```bash
go tool pprof -http=:8080 http://localhost:3000/debug/fgprof
```
