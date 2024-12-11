# Kanatrans

This is a web application that converts an English word to Katakana.

> [!TIP]
> This repository is a fork of [hexium310/kanatrans](https://github.com/hexium310/kanatrans) containing Windows-specific patches.
>
> In order to install this fork on Windows, install the requirements:
>
> * [MinGW-w64](https://www.mingw-w64.org/)
> * [rustup](https://rustup.rs/) with the x86\_64-pc-windows-gnu target
>
> and run the following on Bash:
>
> ```console
> $ cargo install --git https://github.com/chitoku-k/kanatrans --tag=kanatrans/0.2.4-windows --features=vendored --target=x86_64-pc-windows-gnu
> ```

## Dependency

- [flite](https://github.com/festvox/flite)

If the `vendored` Cargo feature is enabled, it compiles and statically links to a copy of flite.

## Usage

```sh
# Get ARPAbet list
$ curl -s localhost:8080/arpabet/kanatrans
{"word":"kanatrans","pronunciation":["k","ae1","n","ax0","t","r","ax0","n","z"]}

# Get Katakana: as a query parameter, pass space-separated ARPAbet to `pronunciation`
# The parameter `word` is optional; if it's set the given `word` will be responded as it is
$ curl -s localhost:8080/katakana --get --data-urlencode pronunciation="k ae1 n ax0 t r ax0 n z"
{"word":null,"pronunciation":"カナトランズ"}

# Oneliner
$ curl -s localhost:8080/katakana --get --data-urlencode pronunciation="$(curl -s localhost:8080/arpabet/kanatrans | jq -r '.pronunciation | join(" ")')"
```
