# Rust Undefined Behavior Example

This repository demonstrates a common source of undefined behavior in Rust: modifying a vector through a raw pointer after its length has been changed.  The code in `bug.rs` showcases this issue, leading to unpredictable results. The corrected version is provided in `bugSolution.rs`.

## Understanding the Issue

Rust's ownership and borrowing system prevents many memory-related errors. However, using raw pointers (`*mut T`) bypasses these safety checks.  When a vector's length changes (e.g., via `push`, `pop`, etc.), the underlying memory allocation might also change.  If a raw pointer to the vector's data is still held, and the vector's data is modified through this pointer after a length change, undefined behavior can occur – the program might crash, produce incorrect results, or seemingly work correctly until it fails unexpectedly.

## Solution

The solution involves avoiding raw pointers whenever possible.  Rust's standard library provides safe alternatives for most common use cases.