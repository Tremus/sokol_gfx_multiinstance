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

-   Main repo: [https://github.com/floooh/sokol](https://github.com/floooh/sokol/commit/d134baeaecfc082deebdd9c9eafd6b8127e926af)
-   Shader compiler repo: [https://github.com/floooh/sokol-tools](https://github.com/floooh/sokol-tools/commit/701f157ed99162b6f296501dce51bf29a893b9bc)
-   Shader compiler recompiled binaries: [https://github.com/floooh/sokol-tools-bin](https://github.com/floooh/sokol-tools-bin/commit/a06f19929ff8f9824ec6dd87c21329b1f205809e)
