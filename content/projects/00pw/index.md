---
date: 2026-05-01
title: "Novi"
cover:
    image: 20200305232406.png
---

Novi is a structured data inspector and validation system. A core library built
in Rust provides a unified interface for parsing many different data types into
a unified structured format. Included with the core library is a validation
system, allowing for user provided Lua scripts (or builtin ones) which are given
the structured data and can perform arbitrary validations and tests on the data,
producing a validation report highlighting any issues with the data. Several
client applications are also included such as a CLI, Web, and Desktop interface,
which all provide interactive interfacees for exploring the parsed structured
data, and the validation reports.

## Core Parsing

The core parsing library is the core of Novi, and being a library it can be
easily integrated into other applications or paired with other clients. Input
data is first transformed, using a chain of transformers, which allows for
handling compressed / encoded content seemlessly. The library provideds a
handler structure for decoding data (the `Decoder`), which provides a rhobust
and flexible interface allowing for the decoding of complex data types, and the
decoder encapsulates all of the complex logic for converting data types and
storing data into the structured tree. The transformed data is passed to the
data format specific parser, which leverages the decoder to read the raw data
into a structured tree, while recording all of the metadata about each field
that was read.

The core parsing is intended to be _extreamly_ forgiving and rhobust. There
should be very few cases that cause a parser to fail and they are more intended
for marshaling the raw data into the defined structure. The checking if it is
valid data (e.g. has resonable values, or the right magic numbers, etc.) is left
up to the validators. This allows for greater flexibility and improved support
for parsing malformed or corrupted data.

## Validation

An addition to the core parsing is the validation. Using an embeded Lua runtime,
the Novi library can support validating the parsed structured tree. Each
supported data format includes builtin validation, but users are also able to
define or overide with their own validations, by simple writing some simple
lua scripts. The validation generates a report with different messages which
reference locations in the structured tree, making it easy through the clients
to annotate the corresponding tree nodes with the validation warnings or errors.

## Clients

The client applications are all designed to be agnostic to the data format being
parsed. The core library and validation handles all of the particularities of
each given format, and by the time the client interactes with the data it is a
generic structured tree and validation report. This make sit very easy to add
support for new formats, since nothing needs to change in any of the clients to
support it.

### Command Line Interface

### Web

The web client compiles the rust library into web assembly to be able to run all
of the parsing and validation client side in the web browser directly. And uses
react and typescript for the interface. It provides a clear interface for
loading new files, and viewing the structured tree of the parsed data.

