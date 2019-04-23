# MacOs Setup

Everytime I get a new Mac, or a collegue starts, there are some fundamental tools and hints I like to share in order to make the setup process seemless.

## Applications

These are some of the tools and apps that are recommended:

1. [iTerm](https://www.iterm2.com/)

Most developers spend their time on the console / terminal.  MacOs already offers a default Terminal, however I personally find iTerm more prowerful.

2. [sdkman.io](https://sdkman.io/install)

Excellent for installing Java (and easily managing the different versions) - plus many other SDKs like gradle, groovy, maven etc.  For example:

```
sdk install gradle
sdk install java 8.0.212-zulu
```

3. [Homebrew](https://brew.sh/)

The missing package manager for macOS.  Excellent for installing awscli, nvm (and managing different versions of node), etc.

```
brew install awscli

brew install nvm
nvm install 8.16.0
nvm alias default v8.16.0
```

4. [Sublime](https://www.sublimetext.com/)

Sublime is a very lightweight text editor, that many have used for coding.  Today, I use Visual Code and IntelliJ for 90% of my code development, but there are many times I need a quick lihght weight text editor to just write some notes, or remove some formatting.

5. [Visual Studio Code](https://code.visualstudio.com/)

Great for web development, front end, ReactJS and GoLang to name a few.

6. [IntelliJ](https://www.jetbrains.com/idea/)

Great for Java, Groovy, Kotlin code bases.

## Aliases

alias ll='ls -la'
alias h=history

## Prompt

Avoid accidently working in the wrong directory, or pushing the wrong branch. Setup your prompt to highlight the path you are in, and the git branch (if any).

Edit your `~/.bash_profile` and add:

```
parse_git_branch() {
     git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}
export PS1="\[\033[32m\]\w\[\033[33m\]\$(parse_git_branch)\[\033[00m\] $ "
```
