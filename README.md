# nvim.d

Forked from [kickstart.nvim](https://github.com/nvim-lua/kickstart.nvim). Kickstart.vim is a small, single file, modular starting point for new users to neovim with a rich documentation to get you from spending long hours configuring neovim to working on projects in minutes. P.S: it is not a neovim distribution.


### Installation

> **NOTE** 
> [Backup](#FAQ) your previous configuration (if any exists)

Requirements:
* Make sure to review the readmes of the plugins if you are experiencing errors. In particular:
  * [ripgrep](https://github.com/BurntSushi/ripgrep#installation) is required for multiple [telescope](https://github.com/nvim-telescope/telescope.nvim#suggested-dependencies) pickers.
* See [Windows Installation](#Windows-Installation) if you have trouble with `telescope-fzf-native`

Neovim's configurations are located under the following paths, depending on your OS:

| OS | PATH |
| :- | :--- |
| Linux | `$XDG_CONFIG_HOME/nvim`, `~/.config/nvim` |
| MacOS | `$XDG_CONFIG_HOME/nvim`, `~/.config/nvim` |
| Windows (cmd)| `%userprofile%\AppData\Local\nvim\` |
| Windows (powershell)| `$env:USERPROFILE\AppData\Local\nvim\` |

Clone kickstart.nvim:

- on Linux and Mac
```sh
git clone https://github.com/nvim-lua/nvim.d.git "${XDG_CONFIG_HOME:-$HOME/.config}"/nvim
```

- on Windows (cmd)
```
git clone https://github.com/nvim-lua/nvim.d.git %userprofile%\AppData\Local\nvim\ 
```

- on Windows (powershell)
```
git clone https://github.com/nvim-lua/nvim.d.git $env:USERPROFILE\AppData\Local\nvim\ 
```

### Windows Installation

Installation may require installing build tools, and updating the run command for `telescope-fzf-native`

See `telescope-fzf-native` documentation for [more details](https://github.com/nvim-telescope/telescope-fzf-native.nvim#installation)

This requires:

- Install CMake, and the Microsoft C++ Build Tools on Windows

```lua
{'nvim-telescope/telescope-fzf-native.nvim', build = 'cmake -S. -Bbuild -DCMAKE_BUILD_TYPE=Release && cmake --build build --config Release && cmake --install build --prefix build' }
```

### Post Installation

Start Neovim

```sh
nvim
```

The `Lazy` plugin manager will start automatically on the first run and install the configured plugins - as can be seen in the introduction video. After the installation is complete you can press `q` to close the `Lazy` UI and **you are ready to go**! Next time you run nvim `Lazy` will no longer show up.

If you would prefer to hide this step and run the plugin sync from the command line, you can use:

```sh
nvim --headless "+Lazy! sync" +qa
```

### Recommended Steps

[Fork](https://docs.github.com/en/get-started/quickstart/fork-a-repo) this repo (so that you have your own copy that you can modify) and then installing you can install to your machine using the methods above.

> **NOTE**  
> Your fork's url will be something like this: `https://github.com/<your_github_username>/nvim.d.git`

### Configuration And Extension

* Inside of your copy, feel free to modify any file you like! It's your copy!
* Feel free to change any of the default options in `init.lua` to better suit your needs.
* For adding plugins, there are 3 primary options:
  * Add new configuration in `lua/custom/plugins/*` files, which will be auto sourced using `lazy.nvim` (uncomment the line importing the `custom/plugins` directory in the `init.lua` file to enable this)
  * Modify `init.lua` with additional plugins.
  * Include the `lua/kickstart/plugins/*` files in your configuration.

You can also merge updates/changes from the repo back into your fork, to keep up-to-date with any changes for the default configuration.

#### Example: Adding a file tree plugin

In the file: `lua/custom/plugins/filetree.lua`, add:

```lua
-- Unless you are still migrating, remove the deprecated commands from v1.x
vim.cmd([[ let g:neo_tree_remove_legacy_commands = 1 ]])

return {
  "nvim-neo-tree/neo-tree.nvim",
  version = "*",
  dependencies = {
    "nvim-lua/plenary.nvim",
    "nvim-tree/nvim-web-devicons", -- not strictly required, but recommended
    "MunifTanjim/nui.nvim",
  },
  config = function ()
    require('neo-tree').setup {}
  end,
}
```

This will install the tree plugin and add the command `:Neotree` for you. You can explore the documentation at [neo-tree.nvim](https://github.com/nvim-neo-tree/neo-tree.nvim) for more information.

### Contribution

Pull-requests are welcome. The goal of this repo is not to create a Neovim configuration framework, but to offer a starting template that shows, by example, available features in Neovim. Some things that will not be included:

* Custom language server configuration (null-ls templates)
* Theming beyond a default colorscheme necessary for LSP highlight groups

Each PR, especially those which increase the line count, should have a description as to why the PR is necessary. Better still, consider contributing back to the main [kickstart repo](https://github.com/nvim-lua/kickstart.nvim).

