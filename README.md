# neovim-config
Home for my personal configuration of NeoVim.

## Why NeoVim?

For those watching my github activity, it's going to look like I just can't figure out what I want.  And they'd be right.  But still, why NeoVim:
  - I do mostly Python development.
  - I don't like full IDEs (e.g. PyCharm)
  - I really like vim keybindings.
  - Magit performance is just unbearable these days in Windows.
  - In theory I can integrate Python REPLs with NeoVim terminals.

## Installation / Setup

For now I'm sourcing NeoVim from chocolatey.  Should likely snag `git.portable`, `fzf` and `neovim` from `choco`.  Then be sure to get the following directories on your `%PATH%`:
  - `c:\tools\git\usr\bin`
  - `c:\tools\git\mingw64\bin`
  - `c:\tools\neovim\neovim\bin`

NeoVim is helping champion `%XDG_CONFIG_HOME%`, so set that somewhere appropriate (e.g. `%UserProfile%`).  Then clone this repo into `%XDG_CONFIG_HOME%/nvim`.

To bootstrap the plugins clone Shougo/dein.vim into `%UserProfile%/repos/vim-plugins/repos/github.com/Shougo/dein.vim`.  Then launch NeoVim and run `:call dein#install()`.

An `Open with NeoVim` entry for Windows Explorer can be created by importing `open_with_neovim.reg` using `regedit` (when ran as administrator).

There is one git default that is worth changing to play ~better with ~Fugitive IMHO.  I prefer to have it infer the desired upstream when I push, and that's not the default to make git noobs be explicit.  To make it the default, change your `.gitconfig` thusly:
`git config --global push.default current`

### PowerShell Notes

These don't really belong here, but I don't feel like making their own home ATM.  Here are some PowerShell tools I'm using to survive my weaning from `cmd.exe`:
  * Don't forget to trust your own scripts: `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned`
  * Grab [posh-git](https://github.com/dahlbyk/posh-git).
    * Install it: `PowerShellGet\Install-Module posh-git -Scope CurrentUser`
    * Load it manually once: `Import-Module posh-git`
    * Then add it to your profile to load everytime: `Add-PoshGitToProfile`
  * Make `conda` work with PowerShell:
    * First check if they ever fixed it to work natively: https://github.com/conda/conda/issues/626
    * Assuming they haven't, likely make use of this community solution: https://github.com/BCSharp/PSCondaEnvs
    * Do so by installing a special conda package into your root environment: `conda install -n root -c pscondaenvs pscondaenvs`
  * Make it possible to load up environment variables from legacy batch scripts.
    * Many PowerShell plugins to do this.  Most provide a function named `Invoke-BatchFile`
    * I'm currently using the (likely overkill) [PowerShell Community Extensions](https://github.com/Pscx/Pscx)
      * Installed way too broadly via: `Install-Module Pscx -Scope CurrentUser`

PowerShell can be used to create a nice shortcut on the Windows taskbar as well.  Make a shortcut to `powershell.exe`, then edit the shortcut to add a custom `.ps1` file as an argument (one that sets up any environment and then calls `nvim-qt.exe --maximized`).  This works better than a `.bat` file (which doesn't seem to want to bring `nvim-qt.exe` into focus).
