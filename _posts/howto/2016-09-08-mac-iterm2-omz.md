---
layout: post
title: Mac - Pimp your iTerm2 with Oh My Zsh
category: How-To
tags: iterm program how-to
description: iterm know how series
---

After you [download][1] and install iTerm2, get the iTerm color setting:

- [Solarized Dark Theme][2] (Recommended)
- [Solarized Light theme][3]
- [More themes @ iterm2colorschemes][4]

Just save it somewhere and open the file(s).

The color settings will be imported into iTerm2. Apply them in iTerm through `iTerm -> preferences -> profiles -> colors -> load presets`.

You can create a different profile other than Default if you wish to do so.

[Original Post][5]

## Oh My Zsh

See [https://github.com/robbyrussell/oh-my-zsh]()

### Install with curl

	sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

When the installation is done, edit `~/.zshrc` and paste with your setting (My favorite theme is [powerlevel9k][8]).

### Install the Powerlevel9k theme

To install this theme for use in Oh-My-Zsh, clone [this][8] repository into your OMZ `custom/themes` directory.

	git clone https://github.com/bhilburn/powerlevel9k.git ~/.oh-my-zsh/custom/themes/powerlevel9k

You then need to select this theme in your `~/.zshrc`, in case you haven't in the prev steps:

	ZSH_THEME="powerlevel9k/powerlevel9k"

For customization, see [here][8], and for other installation method, check [this][9] out.

## Optional settings

### Install powerline patched fonts 

For theme **Agnoster** and **Powerline9k**, [download][6] the fonts and run `./install.sh`.

For theme **Powerline9k**, [download][7] the Non-ASCII font.

### Set iTerm fonts
In iTerm2 `preferences > profile > text`, 

- choose *Underline* cursor
- uncheck **Blinking text allowed**
- uncheck all in *Unicode* section
- change the Font to **14pt Menlo Regular for Powerline**
- check both **Anti-aliased** and **use a different font for non-ASCII text**
- change the Non-ASCII font to **14pt SourceCodePro+Powerline+Awesome Regular**

### AutoSuggestions for Oh My Zsh

1. Clone this repository into `$ZSH_CUSTOM/plugins` (by default `~/.oh-my-zsh/custom/plugins`)

		git clone git://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions

2. Add the plugin to the list of plugins for Oh My Zsh to load (in case you haven't in the prev steps):

		plugins=(zsh-autosuggestions)

3. Start a new terminal session.

Check [this][10] out for more details.

### Enable word jumps

By default, word jumps (option + → or ←) do not work. To enable these, go to `iTerm > Preferences > Profiles > Keys`. Press the `+` sign under the list of key mappings and add the following sequences:

#### Option + right

	⌥→
	Send Escape Sequence
	f

#### Option + left

	⌥←
	Send Escape Sequence
	b

### Shorter prompt style

By default, your prompt will now show `user@hostname` in the prompt. This will make your prompt rather bloated. Optionally set `DEFAULT_USER` in `~/.zshrc` to your regular username (these must match) to hide the `user@hostname` info when you’re logged in as yourself on your local machine. You can get your exact username value by executing `whoami` in the terminal.

### Syntax highlighting

1. Clone this repository in oh-my-zsh's plugins directory

		git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

2. Activate the plugin in ~/.zshrc

		plugins=( [plugins...] zsh-syntax-highlighting)

3. Source `~/.zshrc` to take changes into account

		source ~/.zshrc

[Original post][11]

### When you're done

After changing the value make sure to source your `.zshrc`

	source ~/.zshrc

or just quit and restart your iTerm2 to make sure your changes are picked up.


[1]: http://www.iterm2.com/downloads.html
[2]: https://raw.githubusercontent.com/altercation/solarized/master/iterm2-colors-solarized/Solarized%20Dark.itermcolors
[3]: https://raw.githubusercontent.com/altercation/solarized/master/iterm2-colors-solarized/Solarized%20Light.itermcolors
[4]: http://iterm2colorschemes.com/
[5]: https://gist.github.com/kevin-smets/8568070
[6]: https://github.com/powerline/fonts
[7]: https://github.com/ferdianap/blog/blob/gh-pages/_docs/SourceCodePro%2BPowerline%2BAwesome%2BRegular.ttf
[8]: https://github.com/bhilburn/powerlevel9k
[9]: https://github.com/bhilburn/powerlevel9k/wiki/Install-Instructions#step-1-install-powerlevel9k
[10]: https://github.com/zsh-users/zsh-autosuggestions#oh-my-zsh
[11]: https://github.com/zsh-users/zsh-syntax-highlighting/blob/master/INSTALL.md
