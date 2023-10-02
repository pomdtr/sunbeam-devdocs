# Devdocs (Bash)

## Requirements

- [curl](https://curl.haxx.se/)
- [bkt](https://www.bkt.rs/)

## Install

```bash
curl -L https://raw.githubusercontent.com/pomdtr/sunbeam/main/docs/examples/devdocs/devdocs.bash > ~/.local/bin/sunbeam-devdocs
chmod +x ~/.local/bin/sunbeam-devdocs
```

## Usage

```bash
sunbeam devdocs list-docsets # List all docsets
sunbeam devdocs list-entires --slug <docset-slug> # List all entries for a docset
```
