# Triton - The Go CLI encoder
<p align="center">
<img src="https://github.com/Transmitt0r/triton/assets/7985033/c2939509-96ab-406e-96d9-709e62b6aea0" width="150">
<p align="center">

Triton is a powerful and flexible Go package designed to marshal/encode data structures or utilize a builder pattern to turn data into command line arguments. It's the perfect tool for developers looking to dynamically generate command-line arguments from structured data, offering a more intuitive and programmatic approach compared to traditional command-line argument construction methods.

## Features

- **Easy to Use**: Triton provides a simple and intuitive API to convert your Go structs into command-line arguments.
- **Flexible**: Supports encoding of complex nested structures into a flat command-line argument array.
- **Builder Pattern Support**: Use the builder pattern to incrementally construct command-line arguments in a more readable and maintainable way.
- **Customizable**: Extensive support for custom tags to define how each field is converted into command-line arguments.

## Installation

Install Triton by running:

```sh
go get github.com/Transmitt0r/triton
```

Then import the package in your code:
```go
import "github.com/Transmitt0r/triton"
```

## Usage

There are two ways to use Triton:

1. **Struct Encoding**: Triton can encode a struct into a slice of strings representing command-line arguments. This is similar to how the `encoding/json` package works.
```go
type myCli struct {
  Name string `triton:"entrypoint"`
	Port int    `triton:"flag,port"`
	Path string `triton:"positional"`
}

exampleCli := myCli{
	Name: "app",
	Port: 8080,
	Path: "/home/user",
}

out, err := triton.NewEncoder().Encode(exampleCli)
if err != nil {...}
fmt.Println(out) 
// Output: ["app", "-p", "8080", "/home/user"]
```

2. **Builder Pattern**: Triton can be used to incrementally build command-line arguments using the builder pattern. This is useful when you need to construct command-line arguments dynamically.
```go
out, err := triton.
  NewBuilder().
  WithEntryPoint("app").
  WithFlag("port", 8080).
  WithPositionalArg("/home/user").
  Build()

if err != nil {...}
fmt.Println(out)
// Output: ["app", "-p", "8080", "/home/user"]
```

For a more in-depth guide, please refer to the [documentation]().

## Contributing

We love your input! We want to make contributing to this project as easy and transparent as possible, whether it's:

* Reporting a bug
* Discussing the current state of the code
* Submitting a fix
* Proposing new features

A good starting point is always to create a new Issue.

## License

Triton is open-source software licensed under the [MIT license](LICENSE).
