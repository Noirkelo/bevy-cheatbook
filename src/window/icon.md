{{#include ../include/header012.md}}

# Setting the Window Icon

You might want to set a custom Window Icon. On Windows and Linux, this is
the icon image shown in the window title bar (if any) and task bar (if any).

Unfortunately, Bevy does not yet provide an easy and ergonomic built-in way
to do this. However, it can be done via the `winit` APIs.

The way shown here is quite hacky. To save on code complexity, instead of
using Bevy's asset system to load the image in the background, we bypass
the assets system and directly load the file using the `image` library.

There is some WIP on adding a proper API for this to Bevy; see PRs
[#1163][bevy::1163], [#2268][bevy::2268], [#5488][bevy::5488],
[#8130][bevy::8130], and [Issue #1031][bevy::1031].

This example shows how to set the icon for the primary/main window, from
a Bevy startup system.

```rust,no_run,noplayground
{{#include ../code012/examples/window-icon.rs:main}}
```

Note: that [`WinitWindows`][bevy::WinitWindows] is a [non-send
resource][cb::nonsend].

Note: you need to add `winit` to your project's dependencies, and it must
be the same version as the one used by Bevy. You can use `cargo tree` or
check `Cargo.lock` to see which is the correct version. As of Bevy 0.12,
that should be `winit = "0.28"`. You should also try to match the version
of the `image` library; Bevy uses `image = "0.24"`.
