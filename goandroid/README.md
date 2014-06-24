goandroid
=======

[goandroid](https://github.com/eliasnaur/goandroid) environment.

## Contents

* Ubuntu 12.04 Precise 64bit
* go 1.2 (built from source, `goandroid` patches applied)
* wget
* git
* mercurial
* bzip2
* gcc
* build-essential

## Environment variables

* `HOME`
* `GOROOT`
* `GOPATH`
* `GOANDROID`
* `PATH`

## Volume

`/workspace`

## Working directory

`/workspace`

## Usage

Sample project included in `goandroid` can be built by commands below:

```sh
$ git clone https://github.com/eliasnaur/goandroid.git
$ cd goandroid/hello-gl2/
$ docker run -t -i -v `pwd`:/workspace ksoichiro/goandroid ./build.sh
runtime/cgo
hellogl2
$ cd android
$ ant installd
```

