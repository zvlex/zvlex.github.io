---
title:  "Installing Ruby with asdf on Fedora Linux"
image: assets/images/ruby-fedora.png
tags:
  - Ruby
  - Fedora
---

> I’m using [Fedora Linux](https://getfedora.org/en/) distribution for all examples here, if you are using another system, there may be differences in packages to install.

Let’s begin. 

Open your terminal and run these commands:

```bash
sudo dnf -y groupinstall "Development Tools"
sudo dnf install vim git curl wget zsh util-linux-user 
```

I prefer **zsh** with **ohmyzsh**, so install them too:

```bash
sudo dnf install zsh util-linux-user 
```

Run and make **zsh** your default sh:

```bash
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

If you change a ****command language interpreter (sh) from **bash** to **zsh**, you need to restart your system. Otherwise you can temporally run `zsh` command in terminal and continue.

## Install Ruby with asdf

**[asdf](https://asdf-vm.com/)** - multiple runtime versions manager which supports a lot of programming languages that you can install it in our system, just adding a plugin. It is very simple, flexible and I use it too. 

At first we need to install system dependencies for Fedora Linux

```bash
sudo dnf install -y gcc make bzip2 openssl-devel libyaml-devel libffi-devel readline-devel zlib-devel gdbm-devel ncurses-devel
```

Clone **asdf**

```bash
git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.9.0
```

Open `~/.zshrc` file and add this line to the bottom

```bash
. $HOME/.asdf/asdf.sh
```

Close and open your terminal again. Run `zsh` if you don’t restart your system yet.

Add plugin to **asdf**:

```bash
asdf plugin-add ruby
```

Begin Ruby installation:

```bash
asdf install ruby latest
```

It will end in several minutes (depending on your machine resources).

Then set global Ruby version in you system:

```bash
asdf global ruby latest
```

```bash
ruby -v
=> ruby 3.1.1p18 (2022-02-18 revision 53f5fc4236) [x86_64-linux]
```

You can view a list of any installed programming languages in your system with the command

```bash
$ asdf list                                                                                                                                    ✔ 
=> 
elixir
  1.13.3-otp-24
erlang
  24.3.3
ruby
  3.1.1
```
