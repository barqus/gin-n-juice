Gin-N-Juice Framework
=================

Gin-N-Juice is a Go JSON API framework that is built on [Gin](https://github.com/gin-gonic/gin),
[Gorm](https://gorm.io) and [Goose](https://github.com/pressly/goose). 

Current Features
------
- Uses Gorm as an ORM
- Database migrations via Goose
- Simple routing via Gin
- Simple Auth (login,register,forgot password and reset password)

Requirements
------
- The only mail provider that currently works is Mailgun.
- Go version 1.18 or later

Setup
------
Create a `.env` in the root directory of the project. The required environment variables are:
```
ENCRYPT_KEY=[randomstring]
MAILGUN_DOMAIN=[get from mailgun]
MAILGUN_PRIVATE_KEY=[get from mailgun]
MAILGUN_VALIDATION_KEY=[get from mailgun]
DB_TYPE=[sqlite,postgres or mysql]
DB_CONNECTION_STRING="[connection string for your db]"
```
Add routes to the `routes` directory and reference them in the `routes/router.go`.

Commands
------
- `go run .` or `go run . serve`
  - Runs the webserver
- `go run . migrate [status|up|down|etc...]`
  - Runs goose migrations, see goose's documentation for more details
- `go run . test`
  - Runs tests on all routes currently, plan on testing models also
- `go run . generator -type [model|resource] -name [ex:user] -fields [name:type,name:type,...]`
  - `-fields` is only used with model type
  - resource creates standard API endpoints for the name (create,update,delete,list,view)
  - use singular names, the name will automatically be pluralized when needed (example: `user` not `users`)
  - Example: `go run . generator -type model -name book -fields title:string,category_id:uint,pages:uint`
    - Creates a single file `book.go` in the `/models` directory
  - Example: `go run . generator -type resource -name book`
    - Creates a new directory `/routes/books`
    - Creates five files in that directory
      - `create.go`, `delete.go`, `get.go`, `list.go`, `update.go`
