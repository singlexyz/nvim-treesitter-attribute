## Added attribute query for JSX, Vue, and Svelte filetypes. 





https://github.com/singlexyz/nvim-treesitter-attribute/assets/4456413/8abc9ec8-a906-421e-bfac-ad4242b2d48a

### Summary
[nvim-treesitter-textobjects](https://github.com/nvim-treesitter/nvim-treesitter-textobjects) built-in only supports attribute queries for HTML, Astro, and Heex. 

This plugin adds support for Vue, Svelte, and JSX.

### Usage

After install, Simply add the config to treesitter.

Lazy:
```lua
return {
  "nvim-treesitter/nvim-treesitter",
  build = ":TSUpdate",
  event = "VeryLazy",
  dependencies = {
    { "nvim-treesitter/nvim-treesitter-textobjects" },
    { "singlexyz/nvim-treesitter-attribute" },
  },
  config = function(_, opts)
    require("nvim-treesitter.configs").setup(opts)
  end,
  opts = {
    textobjects = {
      move = {
        enable = true,
        set_jumps = true,
        -- jump by attribute 😳
        goto_next_start = {
          ["]x"] = "@attribute.outer",
        },
        goto_previous_start = {
          ["[x"] = "@block.outer",
        },
      },
      select = {
        enable = true,
        lookahead = true,
        keymaps = {
          -- attribute textobj 🚀
          ["ax"] = "@attribute.outer",
          ["ix"] = "@attribute.inner",
        },
      },
    },
  },
}

```

### Supported
```
     _______ outer
     |     |
<div {...ab} />
<div checked />

_______________________ outer
|                     |
className="abcdefghijk"
className={abcdefghijk}
className={() => set()}
           |         |
           ----------- inner, doesn't include "" or {}
```
