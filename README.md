# SOKOL_GFX (multi-instance)

Fork of [sokol_gfx.h](https://github.com/floooh/sokol/blob/master/sokol_gfx.h) by [@floooh](https://github.com/floooh).

The only difference is all the global state has been removed.

The function `sg_setup` will now return a new instance of `_sg_state_t*`, which you pass to `sg_shutdown` when you want to destroy it. Just about all other functions must now accept a pointer to this state as their first argument.

> [!NOTE]
> Only tested for Windows (DX11) and macOS (Metal)

The context for doing this work was I needed something to work in audio plugins, which demand multiple instanes.

I intend to update this semi-regularly. Basically any time there is a breaking change to the `sokol_gfx` API and its compiler.

-   Main repo: https://github.com/floooh/sokol
-   Shader compiler repo: https://github.com/floooh/sokol-tools
-   Shader compiler recompiled binaries: https://github.com/floooh/sokol-tools-bin

All this renaming of functions is a bit of work. It took me ~2h to get both Win & mac working. Successive updates should be much faster, since all the formatting is kept the same. At the moment updating is still very manual.

TODO: list last commit from sokol & sokol-tools. Consider using sokol-tools-bin as submodule, which will track the commit of the last working compiler.
