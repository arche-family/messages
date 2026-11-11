# Messages

The Arche phone's text messages, written in [Arche](https://github.com/arche-family/arche-lang): a WebAssembly component of the Arche phone's world, built into the phone as one of its default apps and updated from its repository. That world is Nimadir's mini-app world and what a phone adds to it; its WIT is in `wit/` (from arche-os's `phone/wit`), and `world` names it.

It works like Android's:

- The conversations, the latest first, each by its contact's name or its number, over its last message.
- A conversation opened: its messages in order, a message to write, Send and Back.
- A new message: its number and text, and Send, which opens its conversation.
- A message that comes is the phone's notification, which opens Messages.

`manifest` says what it may do: send and read text messages (`messaging`) and read the contacts (`contacts`).

## Build

With [arche-lang](https://github.com/arche-family/arche-lang) checked out next to this repository and built (`make -C stage0 && make -C compiler && make -C wasm`):

```sh
../arche-lang/wasm/nimadir-app.sh . messages.component.wasm
```

## Test

`headless` holds a headless run's input (a number and a text typed, and Send) and the functions the phone's world adds, and `expected.txt` what arche-wasm's interpreter said to them, as Nimadir's shell does not run the phone's world. `app-check.sh` runs the app with arche-wasm, by the interpreter and by the JIT, and compares what it says with `expected.txt`; CI runs it on every push. Messages on the phone itself, through its modem, are tried by arche-os's `tests/phone.sh`.

```sh
../arche-lang/wasm/app-check.sh .
NIMADIR=~/nimadir ../arche-lang/wasm/app-expected.sh .   # expected.txt again, from arche-wasm
```
