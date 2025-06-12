# sokol_gfx.h (multi-instance)

Fork of [sokol_gfx.h](https://github.com/floooh/sokol/blob/master/sokol_gfx.h) by [@floooh](https://github.com/floooh).

The are a few important differences.

1. The global state `_sg_state_t _sg;` has been replaced with a pointer `_sg_state_t* _sg = NULL;`.
2. `sg_setup` returns a new instance of `_sg_state_t*`
3. `sg_shutdown(sg)` accepts the pointer returned by `sg_setup`
4. Before calling into `sg_xxx` functions, you must first set the global state (except `sg_setup` & `sg_shutdown`).

Example program:
```C
struct GUI
{
    int width, height;
    _sg_state_t* _sg;
};
// ...
// init()
gui->sg = sg_setup(/*sg_desc*/);

// ...
// deinit()
sg_shutdown(gui->sg);

// ...
// draw()
sg_set_global(gui->sg);
sg_begin_pass(/*sg_pass*/);

sg_end_pass();
sg_commit();
sg_set_global(NULL);
```

> [!NOTE]
> Only tested for Windows (DX11) and macOS (Metal)

The context for doing this work was I needed something to work in audio plugins, which demand multiple instanes.

I intend to update this repo semi-regularly. 

-   Main repo: [https://github.com/floooh/sokol](https://github.com/floooh/sokol/commit/55af0a43deff7e9907ffeb5112b5c6ed1480bfb7)
-   Shader compiler repo: [https://github.com/floooh/sokol-tools](https://github.com/floooh/sokol-tools/commit/6ddf2a1ba5cce0afa2fed91835930a4e4eb9fc3b)
-   Shader compiler recompiled binaries: [https://github.com/floooh/sokol-tools-bin](https://github.com/floooh/sokol-tools-bin/commit/90d2b9267813cbfb66e26c8e3eca5cc866f947e0)
