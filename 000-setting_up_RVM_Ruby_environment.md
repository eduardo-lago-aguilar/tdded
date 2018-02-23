# Setting up RVM / Ruby Environment

## Install `build-essential`
```bash
sudo apt -y install build-essential
```

## Install `libpq-dev` for `postgresql`
```bash
sudo apt -y install libpq-dev
```

## Install `NodeJS 9.x+`
- See [Node.js v9.x](https://github.com/nodesource/distributions#installation-instructions) 

## Install RVM

### Install RVM GPG keys
```bash
curl -sSL https://rvm.io/mpapis.asc | gpg2 --import -
```

### Install Stable RVM
```bash
curl -sSL https://get.rvm.io | bash -s stable
```

### Check PATH for RVM 
```bash
grep -i  rvm ~/.profile ~/.mkshrc ~/.bashrc ~/.zshrc  ~/.bash_profile ~/.zlogin
rvm --version
```

### Check RVM environment before installing Ruby
```bash
rvm info
```

## Install Ruby

### List installed intrepreters
```bash
rvm list
```

### List available interpreters
```bash
rvm list known
```

### Current ruby version before installing Ruby
```bash
rvm current
```

### Install Ruby
```bash
rvm install ruby-2.4.1
```

### Check installed Rubies & RVM environment (again)
```bash
rvm list
rvm info
```

### Set a ruby as the user default
```bash
bash --login # allow login shell
rvm use ruby-2.4.1 --default
```

*NOTE*: alternatively to login shell, user can logout & login again

### Check installed Rubies, current Ruby & RVM environment (yes, again!)

```bash
rvm list
rvm current
rvm info
```

### Ensure RVM is available in non login sessions
Append this line to `~/.bashrc` or `~/.bash_profile` if not present, line can be copied from `~/.profile` as well:
```bash
[[ -s "$HOME/.rvm/scripts/rvm" ]] && source "$HOME/.rvm/scripts/rvm" # Load RVM into a shell session *as a function*
```

### Check binaries
Open a new terminal and enter:
```bash
ruby --version
irb --version
gem --version
rake -version
```
