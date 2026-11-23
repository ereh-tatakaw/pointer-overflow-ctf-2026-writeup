# The Apparatus, Manifestation

**Category:** EXPLOIT  
**Wave:** 8

## Overview

The challenge presents a note-taking service that allows users to create, read, erase, and amend notes. Hidden within the provided binary is a function that reveals the flag.

The goal is to investigate the program's memory handling and find a way to reach that function through the available interface.

## Analysis

The most interesting operation is amending an existing note. Examining how the program handles changes to a note's body reveals a memory-safety issue. The new input length is not properly checked against the original allocation.

The binary also uses an indirect callback when a note is read. This makes the relationship between note storage, adjacent memory, and callback execution worth investigating.

The executable is non-PIE, and the challenge provides additional information at connection time that may be useful during analysis.

## Approach

My solution involved examining the binary and identifying the hidden flag function, tracing how note structures and their callbacks are stored, investigating the consequences of supplying an oversized body during an amendment, and using the resulting memory corruption to redirect program execution.

The important part was not only finding the hidden function but also understanding how the vulnerability interacted with the program's data layout.

## Flag

POCTF{126.390.****************.**************************}

Note: Writeup was done with the assist of ChatGPT.
