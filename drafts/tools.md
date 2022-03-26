# Tools

## Developer Tools (CLI)

- [Bat](https://github.com/sharkdp/bat) - A cat(1) clone with syntax highlighting and Git integration.
  - `brew install bat`
- [Brew](https://brew.sh) - Package Manager
  - `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`
  - This will take a while.
- [exa](https://the.exa.website/) - A modern replacement for ls.
  - `brew install exa`
- [Fuzzy Find (fzf)](https://github.com/junegunn/fzf)
  - `brew install fzf`
- [gitter](https://github.com/elifiner/gitter) - adds non-intrusive interactive menus to the common git commands
  - `sudo pip install gitter`
- [grc/grcat](https://github.com/garabik/grc) - Generic Colorizer
  - `brew install grc`
- [ImageMagick](https://imagemagick.org/) - Create, edit, compose, or convert digital images.
  - `brew install imagemagick`
  - Example: `convert -loop 0 -delay 100 *.png out.webm ':include :type=video controls height=400px width=100%'`
- [jless](https://jless.io/) - a command-line JSON viewer
  - `brew install jless`
- [jq]() - lightweight and flexible command-line JSON processor
  - `brew install jq`
- [nvm](https://github.com/nvm-sh/nvm#installing-and-updating) - Node Version Manager
  - `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash`
- [Pandoc](https://pandoc.org/) - A universal document converter
  - `brew install pandoc`
- [Powerlevel10k](https://github.com/romkatv/powerlevel10k#homebrew) - A zsh theme
  - `brew install romkatv/powerlevel10k/powerlevel10k`
  - `echo "source $(brew --prefix)/opt/powerlevel10k/powerlevel10k.zsh-theme" >>~/.zshrc`
  - `p10k configure`
- [Rich CLI](https://github.com/Textualize/rich-cli) - A command line toolbox for fancy output in the terminal
- [termenu](https://github.com/elifiner/termenu) - A command line utility and Python library for displaying console based interactive menus
  - Install via gitter (above)
- [Volta]()
  - `curl https://get.volta.sh | bash`
- [xml2](https://web.archive.org/web/20160719191401/http://ofb.net/~egnor/xml2/) - Makes XML and HTML more amenable to classic UNIX text tools
  - `brew install xml2`
- [xq / yq](https://github.com/kislyuk/yq) - jq wrapper for YAML, XML, TOML documents
  - `pip3 install yq`
  - Using docker image to update project version in a pom.xml:
    - `docker run --rm -v "${PWD}":/workdir mikefarah/yq -px -ox '.project.version |= "MAJOR.MINOR.BUILD"' pom.xml`
- [Yarn]() - Node Package Manager
  - `npm install -g yarn`

## Developer Tools (GUI)

- [Android Studio](https://developer.android.com/studio/)
  - `brew install --cask android-studio`
- Docker
  - `brew install --cask docker`
- [Iterm2](https://iterm2.com) - Terminal
  - `brew install --cask iterm2`
- [Postman](https://www.postman.com/) - HTTP Utility
  - `brew install --cask postman`

## UI Utilities

- [AltTab](https://alt-tab-macos.netlify.app/) - Window Switcher
  - `brew install alt-tab`
- [Kap](https://getkap.co/) Screen Recorder
  - `brew install --cask kap`
- [Karabiner Elements](https://karabiner-elements.pqrs.org/) - Keyboard Customizer, can disable built-in keyboard upon having another
- [KeyCastr](https://github.com/keycastr/keycastr) - An open-source keystroke visualizer
  - `brew install --cask keycastr`
- [LiceCAP](https://www.cockos.com/licecap/) - Simple animated screen captures
  - `brew install --cask karabiner-elements`
- [Rectangle](https://rectangleapp.com/) - Window Manager (replaces Spectacle)
  - `brew install --cask rectangle`
  - Uncheck "Move to adjacent display..." in its preferences.
- [Scroll-Reverser](https://pilotmoon.com/scrollreverser/) - Reverses direction of scrolling with independent settings for trackpads and mice
  - `brew install --cask scroll-reverser`

## Applications

- [Audacity](https://www.audacityteam.org/) - Audio Software
  - `brew install --cask audacity`
- [Boxy SVG](https://boxy-svg.com/) - SVG Editor
- [Quip](https://quip.com/) - Living Documents
  - `brew install --cask quip`

## Chrome Extensions

- [Snippets](https://chrome.google.com/webstore/detail/snippets/fakjeijchchmicjllnabpdkclfkpbiag)

## IDEA Themes

- [VSCode Dark Plus Theme](https://plugins.jetbrains.com/plugin/12255-visual-studio-code-dark-plus-theme) - Install it as a plugin (not a theme)
