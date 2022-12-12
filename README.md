# lugl
lua + lvgl = lugl

lugl is currently under development. A flappy bird game is ready for showoff. See simulator instructions below.

<p align="center">
  <img src="https://i.ibb.co/nbgYvZW/flappybird.gif" />
</p>

## Introduction

lugl is a wrapper around lvgl core functions and widgets with class inherence in mind, which is lvgl trying to do in `C`. Lua makes widgets inherence smoothly.

```lua
local root = lugl.Object()

-- create obj on root
local obj = root:Object()

-- create image on root and set position/img src/etc. properties.
local img = root:Image{
    src = "res/image.png",
    x = 0,
    y = 0,
    bg_color = 0x004400,
    pad_all = 0
}

-- change image properties.

img:set{
    x = 100,
    y = 100,
    src = "res/another.png"
}

-- create Label on root and set its font
local label = root:Label{
    text = string.format("Hello %03d", 123),
    text_font = lugl.Font("MiSansW medium,, montserrat", 24, "normal"),
    align = {
        align = CONST.align.CENTER,
        x_ofs = 0,
        y_ofs = 100,
    }
}


```

LUGL mainly targets for embedded device, a simulator on Ubuntu has been provided for preview.

### Embedded device

For embedded device, assume the lvgl environment has already been setup, simply add the `lugl.c` to sources for compiling. And make sure `luaopen_lugl` is added to global lib. Below is example from `simulator/main.c` shows this exact method.

```c
  luaL_requiref(L, "lugl", luaopen_lugl, 1);
  lua_pop(L, 1);
```

### PC simulator

Currently compile lugl to `so` is not available, lugl depends on lvgl and various configurations(`lv_conf.h`).
The simulator provided in this repo can be used as example if lugl is required on PC.

Make sure clone the submodules, lugl simulator comes directly from lvgl simulator with lua added.

```
git clone --recursive https://github.com/XuNeo/lugl.git
```

#### Dependencies

To run simulator on PC, make sure `lua` header is available, you may need to install below packages.

```
sudo apt install libsdl2-dev lua5.3 liblua5.3-dev
```

Both lua5.3 and lua5.4 are supported. Versions below 5.2 has not been verified.



