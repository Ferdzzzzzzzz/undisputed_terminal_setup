# Mac Terminal Setup
### by Ferdzz

This is the ultimate, undisputed terminal setup for mac…use responsibly.

## iTerm

Download [iTerm](https://www.iterm2.com/)

OR

    brew cask install iterm2
    
  ## Keyboard Layout
  
  First one is simple, just some navigation shortcuts so that you can work faster.
  
    1. Go to `Preferences->Profiles->Keys` (NOT `Preferences->Keys`)
    2. Press `Presets`
    3. Select `Natural Text Editing`
    
Then, you can move a word backwards using Option ⌥ + ← and a word forwards using Option ⌥ + →, move to the start of the       line using fn + ← and to the end of the line with fn + →. Also you can delete a word backwards using Option ⌥ + ⌫, delete the whole line using Command ⌘ + ⌫.
  
  ## Zsh
  
 If you’re using anything before macOS Catalina, your default shell will be bash. If your macOS is Catalina or newer, your default should be vanilla zsh. You can run echo $0 in your terminal to check. Either way, we aren’t using vanilla zsh, we want to use a distribution called [ohmyzsh](https://github.com/robbyrussell/oh-my-zsh) . This gives us a bunch of cool plugins and shit. First, if you don’t already have Zsh installed, do it and make it your default shell:
 
    brew install zsh

    chsh -s $(which zsh)

Then install oh-my-zsh:

    sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

In your home directory you can now see a .zshrc file as well as .zshrc.pre-oh-my-zsh, if you had any zsh config that you wanted to save, it’ll be safe and sound in your pre-oh-my-zsh file...you can just copy it over. Then add this to the .zshrc:

    export ZSH=”/Users/<username>/.oh-my-zsh”
    source $ZSH/oh-my-zsh.sh

## Plugins

OhMyZsh has a couple of cool plugins that does auto-complete for you, this is my recommendation (the stack that I use at least)...obviously add it to your .zshrc config file.

    plugins=(git docker docker-compose npm brew z yarn nvm)

Feel free to check out [more plugins](https://github.com/robbyrussell/oh-my-zsh/tree/master/plugins) for yourself...warning, there is literally like...a hundred or something: 

## Powerlevel9k

By now your terminal should be feeling better but still looking a bit kak. So we’re going to add the  **PowerLevel9k** theme to your terminal to make it look pretty. Run the following command in your terminal:

    git clone https://github.com/bhilburn/powerlevel9k.git ~/.oh-my-zsh/custom/themes/powerlevel9k

That just clones the theme into your ohmyzsh directory. Then add the following to your .zshrc file:

    ZSH_THEME="powerlevel9k/powerlevel9k"
    source /usr/local/opt/powerlevel9k/powerlevel9k.zsh-theme

## NerdFont

Now we just want to add a font to make your terminal more readable, we’re going to add [NerdFonts](https://github.com/ryanoasis/nerd-fonts): 

    brew tap homebrew/cask-fonts
    brew cask install font-hack-nerd-font

After installing nerd-font, add this to your .zshrc:

    POWERLEVEL9K_MODE='nerdfont-complete'

Then, open iTerm and do this:

    1. Press CMD ,
    2. Go to Profiles>Text
    3. Click Change Font 
    4. Select Hack Nerd Font

## Material Color Theme

Almost there, your terminal is feeling awesome now...but the colors are probably sore on your eyes hey? Let’s take care of that…

Download the material color theme in a directory of your choice:

    curl -O https://raw.githubusercontent.com/MartinSeeler/iterm2-material-design/master/material-design-colors.itermcolors

Then:

    1. Go to iTerm2 > Preferences > Profiles > Colors Tab
    2. Click Color Presets (bottom right)
    3. Click import
    4. Select material-design-colors.itermcolors
    5. Select material-design-colors from Load Presets.

## Roundup

So for the last step we just want to configure the theme to our liking (or at least my liking), and I’ll just give you some recommended shortcut aliases that you can add in your .zshrc for a faster workflow.

This is to make your terminal a bit more readable (shows branch management etc.)

    POWERLEVEL9K_SHORTEN_DIR_LENGTH=2
    POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS=(vcs)
    POWERLEVEL9K_LEFT_PROMPT_ELEMENTS=(dir)

If you're a Node developer, firstly, consider switching to Dart/Golang, if you're not going to do that, then add this config to your terminal for nvmrc (Node version manager) to work automatically:

    HYPHEN_INSENSITIVE="true"
    export NVM_DIR="$HOME/.nvm"
    [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
    [ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
    # place this after nvm initialization!
    autoload -U add-zsh-hook
    load-nvmrc() {
      if [[ -f .nvmrc && -r .nvmrc ]]; then
        nvm use
      elif [[ $(nvm version) != $(nvm version default)  ]]; then
        echo "Reverting to nvm default version"
        nvm use default
      fi
    }
    add-zsh-hook chpwd load-nvmrc
    load-nvmrc
  
Add some aliases to speed up your workflow (NB. don't add spaces outside of quoutes, this is a C compiler(I think), so it'll break):

    alias myWorkFolder="cd ~/some/directory/where/your/work/is"
    alias c="clear"
    alias src="source ~/.zshrc"

The last alias is quite nifty, if I make changes to my .zshrc I don’t need to exit the terminal or reload it, I simply type src and the changes are there. Useful for anyone that works in their .zshrc file often.

Some useful shortcuts that should be working already (thanks to oh-my-zsh and plugins):

    .. -> cd ..
    gl -> git pull
    gp -> git push
    gf -> gith fetch
    dcu -> docker-compose up

...and many more, go read through plugin docs mentioned earlier.

Some more Zsh configuration flags:

    HYPHEN_INSENSITIVE="true"

## Bonus: Optional Hotkey Window

To add a hotkey (quick popup shortcut key), go to settings (CMD ,):
Then navigate to Profiles->Keys
Click, Configure Hotkey Window
Select a hotkey of your choice, then to avoid extreme annoyance maybe tick Pin hotkey window…
Enjoy your new super easily accessible terminal :D 

## Fin

Now that your terminal is sick, you can go around looking like a badass, enjoy your awesome new dev setup :)

### Sources:

If anything wasn’t clear...then this is the [article](https://medium.com/@rafavinnce/iterm2-zsh-oh-my-zsh-material-design-the-most-power-full-terminal-on-macos-332b1ee364a5) that I summarized:

The official docs that I linked throughout are also not too bad, but can be a bit overwhelming for an initial setup.

## Cool Nugget

    brew install neofetch
    neofetch -s
  
Tells you some cool shit about your system and looks pretty :)

![My Terminal](/terminal.png)


## Error Solving

* Folder permission "Insecure completion-dependent directories detected"

```
chmod 755 /usr/local/share/zsh
chmod 755 /usr/local/share/zsh/site-functions
```














