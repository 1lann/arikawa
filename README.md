# arikawa

[![Godoc Reference](https://img.shields.io/badge/godoc-reference-blue?style=flat-square                  )](https://godoc.org/github.com/diamondburned/arikawa)
[![       Examples](https://img.shields.io/badge/Example-__example%2F-blueviolet?style=flat-square       )](https://github.com/diamondburned/arikawa/tree/master/_example)
[![Discord Gophers](https://img.shields.io/badge/Discord%20Gophers-%23arikawa-%237289da?style=flat-square)](https://discord.gg/7jSf85J)
[![   Hime Arikawa](https://img.shields.io/badge/Hime-Arikawa-ea75a2?style=flat-square            )](https://hime-goto.fandom.com/wiki/Hime_Arikawa    )

A Golang library for the Discord API.

## Examples

### [Simple](https://github.com/diamondburned/arikawa/tree/master/_example/simple)

Simple bot example without any state. All it does is logging messages sent into
the console. Run with `BOT_TOKEN="TOKEN" go run .`

### [Undeleter](https://github.com/diamondburned/arikawa/tree/master/_example/undeleter)

A slightly more complicated example. This bot uses a local state to cache
everything, including messages. It detects when someone deletes a message,
logging the content into the console.

This example demonstrates the PreHandler feature of this library. PreHandler
calls all handlers that are registered (separately from session), calling them
before the state is updated.

## Comparison: Why not discordgo?

Discordgo is great. It's the first library that I used when I was learning Go.
Though there are some things that I disagree on. Here are some ways that this
library is different:

- Better package structure: this library divides the Discord library up into
smaller packages.
- Cleaner API/Gateway structure separation: this library separates fields that
would only appear in Gateway events, so to not cause confusion.
- Automatic un-pagination: this library automatically un-paginates endpoints
that would otherwise not return everything fully.
- Flexible underlying abstractions: this library allows plugging in different
JSON and Websocket implementations, as well as direct access to the HTTP 
client.
- Flexible API abstractions: because packages are separated, the developer could
choose to use a lower level package (such as `gateway`) or a higher level
package (such as `state`).
- Pre-handlers in the state: this allows the developers to access items from the
state storage before they're removed.
- Pluggable state storages: although only having a default state storage in the
library, it is abstracted with an interface, making it possible to implement a
custom remote or local state storage.
- No code generation: just so the library is a lot easier to maintain.

## You-should-knows

- The bot will fatally exit if it fails to reconnect to the Gateway after a
certain amount of times. This is changeable in `gateway.WSFatal`, or
`(*Gateway).FatalLog`.

## Testing

The package includes integration tests that require `$BOT_TOKEN`. To run these
tests, do

```sh
export BOT_TOKEN="<BOT_TOKEN>"
go test -tags integration ./...
```
