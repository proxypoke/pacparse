pacparse
========

Overview
--------

An argparse-like library for creating CLI-applications with pacman-style command
syntax.

pacman - Arch's package manager - has a very unique style of command line
arguments. It has multiple modes represented with upper-case letters, with one
having to be presented. Each mode has some options and switches, in addition to
some global flags which can be used in any mode.

This syntax is convenient, intuitive and powerful, but unfortunately impossible
to emulate with argparse - which is why this lib is being written.

BNF
---

This is a (pseudo-)BNF which describes the pacman argument syntax.

    <call> ::= [<opts> <whitespace>] <mode> [<whitespace> <opts>]
    <mode> ::= "-" [<switches>] <uppercase> [<switches>] <whitespace> [<args>] |
                "-" <uppercase> <opt>  |
                <longopt> [<whitespace> <args>]
    <opts> ::= "-" <opt> | <longopt> [<whitespace> <args>]
    <opt> ::= [<switches>] <lowercase> [<switches>] <whitespace> <args>
    <longopt> ::= "--" <word>
    <switches> ::= <lowercase> [<switches>]
    <args> ::= <word> | <nargs> 
    <nargs> ::= <word> [<nargs>]
