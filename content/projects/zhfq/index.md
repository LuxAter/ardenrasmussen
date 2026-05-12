---
date: 2026-02-23
title: "Nand to Tetris"
editPost:
    URL: https://github.com/Nedra1998/Nand2Tetris
    Text: https://github.com/Nedra1998/Nand2Tetris
---

Nand to Tetris is a course from the book _The Elements of Computing Systems:
Building a Modern Computer from First Principles_ by Noam Nisan and Shimon
Schocken. The course covers the design and implementation of a simplified
computer model, starting from first principles of a single NAND gate, and using
that to build up more complex logic gates. Gradually expanding on the previous
chapters to introduce more complex structures ultimately culminating in the
construction of a basic computer.

Then going beyond the basic computer on the hardware side of the equation it
also introduces and develops the core software stack for interacting with the
computer. Building up an assembler, a virtual machine, and even a compiler for a
higher-level Java like language.

This project is my following along of the course, implementing the hardware in
the Nand2Tetris Hardware Definition Language (HDL), and the software stack in
Rust from scratch using no dependencies for the lexing or parsing. After
completing the entire course the repository provides a functional HDL
definition for the computer, and a fully featured software stack providing
everything needed to write Jack (the high-level Java like language) programs
and compile them to run on the simulated hardware.
