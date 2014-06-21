pandoc
========

## Contents

* Ubuntu 12.04 Precise 64bit
* TexLive
* Haskell Platform
* Pandoc

## Usage

    docker run -t -i -v `pwd`:/workspace ksoichiro/pandoc pandoc sample.md -s -o sample.html
