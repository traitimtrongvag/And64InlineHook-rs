# And64InlineHook-rs

A Rust library for inline hooking on ARM64/AArch64. It allows runtime patching of functions and optional trampoline to call the original code.

## Features
- Patch ARM64 instructions and redirect execution
- Thread-safe trampoline pool
- Works on Android and other ARM64 platforms

## Safety
All functions are unsafe: they modify executable memory and use raw pointers.

## Example

```rust
use and64inlinehook::{init_hook_pool, a64_hook_function};

unsafe {
    init_hook_pool();
    let target_fn = some_function as *mut u32;
    let hook_fn = my_hook as *const u32;
    if let Some(trampoline) = a64_hook_function(target_fn, hook_fn) {
        // Hook installed, trampoline can call original
    }
}