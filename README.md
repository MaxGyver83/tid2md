# tid2md

Migrate your TiddlyWiki5 (Node.js version) tiddlers (`.tid` files) to Markdown tiddlers (`.md` files for markup plus `.md.meta` files for meta information).


## Markdown in TiddlyWiki

[TiddlyWiki](https://tiddlywiki.com/) uses its own [WikiText](https://tiddlywiki.com/#WikiText) markup language. While this is the natural first choice when using TiddlyWiki, it's also possible writing tiddlers in Markdown using the official [Markdown Plugin](https://tiddlywiki.com/#Markdown%20Plugin). Markdown has the advantage that it's used in many places (p.e. GitHub, GitLab, BitBucket, StackOverflow, Reddit) and is supported by many editors, parsers and other tools. When you often copy tiddlers (or parts of them) to other websites or when you edit/process your `.tid` files with tools except TiddlyWiki itself, it might make sense to write your tiddlers in Markdown or migrate those already written in WikiText to Markdown. This is what `tid2md.py` was made for.


## Installation

Just clone this repository and copy/symlink `tid2md.py` to a directory in your `$PATH`.

For example (on Linux):

```sh
cd ~/Downloads
git clone https://github.com/MaxGyver83/tid2md.git
mkdir -p ~/.local/bin
cd ~/.local/bin
ln -s ~/Downloads/tid2md/tid2md.py
cd ~
test -f tid2md.py || PATH=~/.local/bin:"$PATH"
```


## How to use tid2md.py

`tid2md.py` is a Python script to be run in a terminal. It takes a list of `.tid` files as input parameter. This means that it cannot be used with a single-HTML-file TiddlyWiki. It only works with a [Node.js TiddlyWiki](https://tiddlywiki.com/#Installing%20TiddlyWiki%20on%20Node.js) which stores every tiddler as a separate `.tid` file on your disk.

⚠ **Warning: This script was only tested by myself using my own tiddlers. Please test it on a copy of your wiki and check if the migrated tiddlers look like expected.**

### Migrate all `.tid` files:

```sh
cd path/to/wiki/tiddlers
tid2md.py --delete *.tid
```

This will create Markdown tiddlers (consisting of a `.md` and a `.md.meta` file) for all WikiText tiddlers except:

* System tiddlers
* Tiddlers containing macro definitons
* Tiddlers containing at least one table

Tiddlers with tables are skipped by default because Markdown tables are lacking many features of WikiText tables (p.e. two header rows, captions, cell alignment, cell merging, ...). Use `--tables` to migrate such tiddlers anyway.

The `--delete` option makes the script delete the original `.tid` files after a successful migration because otherwise you would end up with two versions of the same tiddler.

Run `tid2md.py --help` for more options.


## Performance

On my laptop, it takes about 370 ms to migrate 503 tiddlers (+ skipping 146 tiddlers).
