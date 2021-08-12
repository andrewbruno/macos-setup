# MacOs Setup

Everytime I get a new Mac, or a collegue starts, there are some fundamental tools and hints I like to share in order to make the setup process seemless.

## Applications

These are some of the tools and apps that are recommended:

0. [Xcode](https://developer.apple.com/xcode/) Tools

Ensure you have a proper compilation toolchain
```
xcode-select --install
```

1. [iTerm](https://www.iterm2.com/)

Most developers spend their time on the console / terminal.  MacOs already offers a default Terminal, however I personally find iTerm more prowerful.

2. [sdkman.io](https://sdkman.io/install)

Excellent for installing Java (and easily managing the different versions) - plus many other SDKs like gradle, groovy, maven etc.  For example:

```
sdk install gradle
sdk install java 8.0.282-zulu
sdk install java 11.0.9-amzn
```

3. [Homebrew](https://brew.sh/)

The missing package manager for macOS.  Excellent for installing awscli, maven, nvm (and managing different versions of node), etc.

For Node apps or ReactJS apps:
```
brew install nvm
nvm install v12.18.4
nvm alias default v12.18.4
nvm use default
```
Note: Check AWS supports runtime [versions|https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtimes.html] in order to match.

Others:
```
brew install awscli
brew install maven
brew install golang
```

4. [Atom](https://atom.io/)

Atom is a very lightweight text editor, that many have used for coding.  Today, I use Visual Code and IntelliJ for 90% of my code development, but there are many times I need a quick lihght weight text editor to just write some notes, or remove some formatting.

5. [Visual Studio Code](https://code.visualstudio.com/)

Great for web development, front end, ReactJS and GoLang to name a few.

6. [IntelliJ](https://www.jetbrains.com/idea/)

Great for Java, Groovy, Kotlin and Golang code bases.

Use Golang plugin https://plugins.jetbrains.com/plugin/9568-go

7. Enable Developer Mode using XCode

This assists in the debugger not asking for admin privilages everytime you attempt to run Delve or other debuggers.

```
sudo /usr/sbin/DevToolsSecurity -enable
```

## Aliases

Edit your `~/.zshrc` file and add some good old aliases:

`vi ~/.zshrc`

and add these at the top:

```
alias ll='ls -la'
alias h=history
```

## Add Git/branch prompt

Avoid accidently working in the wrong directory, or pushing the wrong branch. Setup your prompt to highlight the path you are in, and the git branch (if any).

The following gives you a prompt like:

```~/dev/andrewbruno/macos-setup (master) $```

Edit your `~/.zshrc` and add:

```
parse_git_branch() {
     git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}
export PS1="\[\033[32m\]\w\[\033[33m\]\$(parse_git_branch)\[\033[00m\] $ "
```

## Add support for Makefile command complete

Edit your `~/.zshrc` and add:

```
zstyle ':completion:*:*:make:*' tag-order 'targets'
autoload -U compinit && compinit
```

## Add ssh command complete

Add to your to your `~/.zshrc`:

```
_ssh()
{
    local cur prev opts
    COMPREPLY=()
    cur="${COMP_WORDS[COMP_CWORD]}"
    prev="${COMP_WORDS[COMP_CWORD-1]}"
    opts=$(grep '^Host' ~/.ssh/config | awk '{print $2}')
    COMPREPLY=( $(compgen -W "$opts" -- ${cur}) )
    return 0
}
complete -F _ssh ssh
```

In your .ssh/config file add mappings:

```
Host mars-prd
 Hostname mars.prd.universe
 IdentityFile ~/.ssh/id_rsa
 ForwardAgent yes

Host 10.*
  IdentityFile ~/.ssh/id_rsa
  ProxyCommand ssh -tW %h:%p mars-prd
```
