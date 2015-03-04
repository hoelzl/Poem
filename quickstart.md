---
title: Poem Quickstart
subtitle: Getting started with Poem in Lua
---

Writing XBTs using the Lua implementation is the simplest way to get
started with Poem.

Installation
------------

You need to have a working Lua installation; if you want to run the
examples from the XBT repository you should use LuaJIT since some of
the libraries exist only for LuaJIT. Clone the `Xbt.lua` from its
[GitHub repository](https://github.com/hoelzl/Xbt.lua) and ensure that
your `LUA_PATH` environment variable contains the path to the
`Xbt.lua` module. If you use OS X or Linux with the `bash` shell, your
`.bashrc` should probably include a line of the form

    export LUA_PATH="$LUA_PATH;.../xbt/?.lua;.../xbt/?/init.lua"

(where `.../xbt` is the path to the `Xbt.lua/src` folder).
