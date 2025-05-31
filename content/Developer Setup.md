Whenever I set up a new system, no matter which platform, here are some snippets which help me, and this is just a quick way for me to reference them so I can just quickly copy and paste whatever I need —pick out the cherry from the basket.

## CLI

### Fish shell

install https://starship.rs

```fish
curl -sS https://starship.rs/install.sh | sh
```

install https://github.com/jorgebucaran/fisher

```
curl -sL https://raw.githubusercontent.com/jorgebucaran/fisher/main/functions/fisher.fish | source && fisher install jorgebucaran/fisher
```

```fish
fisher install jethrokuan/z
fisher install jorgebucaran/autopair.fish
fisher install jorgebucaran/replay.fish
fisher install meaningful-ooo/sponge
fisher install franciscolourenco/done
```

configure aliases

```shell
alias --save ls eza
alias --save l "ls -la --icons"
alias --save la "ls -la --icons"
alias --save ll "ls -la --icons --tree"
alias --save cat "bat -pp"
alias --save vi nvim
alias --save vim nvim
alias --save pm pnpm
alias --save px pnpx
alias --save tree "eza --tree"
```

function for navigating between repositories in ghq

```shell title=".config/fish/functions/ghq-repo.fish"
function ghq-repo --description 'Navigate to remote repository'
  if begin; set -q argv[1]; and test -d "$(ghq root)/$argv[1]"; end
    cd "$(ghq root)/$argv[1]"
    return 0
  end

  set path (ghq list --full-path --bare | fzf --delimiter / --with-nth -2..-1 --preview 'echo {}' --preview-window down:2)

  if not test -z "$path"
    cd "$path"
  end
end
```

function for finding and cleaning up residual files after uninstalling apps

```shell title=".config/fish/functions/remove-residual-files.fish"
function remove-residual-files --description 'Search for files excluding common directories, then select and move chosen files to the system trash.'
  fd "$argv" --hidden -E .Trash -E Documents -E "The Pile" -E "Downloads" -E "/System" / | \
    fzf -m | \
    xargs -I {} trash {}
end
```

