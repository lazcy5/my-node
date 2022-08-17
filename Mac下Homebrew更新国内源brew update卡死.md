##### Mac下Homebrew更新国内源brew update卡死

###### 先更新下brew

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

###### 再更新国内源

```bash
#更新Homebrew
cd "$(brew --repo)"
git remote set-url origin https://mirrors.ustc.edu.cn/brew.git

#更新Homebrew-core
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-core.git

#更新Homebrew-cask（最重要的一步，很多更新完国内源依然卡就是没更新这个）
cd "$(brew --repo)"/Library/Taps/homebrew/homebrew-cask
git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-cask.git
```

###### 更新HOMEBREW_BOTTLE_DOMAIN

最重要

- 使用zsh的用户

```bash
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles/' >> ~/.zshrc
source ~/.zshrc
```

- 使用bash的用户

```bash
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles/' >> ~/.bash_profile
source ~/.bash_profile
```

更新库

```bash
brew update -v
#或都使用下面的更新
brew update-reset 
```

