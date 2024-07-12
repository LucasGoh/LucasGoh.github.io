---
title: how to write github blog using jekyll on macOS
categories: [tool]
---
## Download tools
follow this instruction: https://jekyllrb.com/docs/installation/macos/

## Change ruby version using chruby

Afte Ruby is installed, add these 2 lines on ~/.bash_profile. If you’re using ZSH as your shell, add these to ~/.zshrc.
```bash
source  /opt/homebrew/opt/chruby/share/chruby/chruby.sh
source  /opt/homebrew/opt/chruby/share/chruby/auto.sh
```
chruby.sh enables chruby. To switch to a Ruby version, run
```bash
chruby 3.3.3
```

Then check version
```bash
ruby -v
```

## Running local server
Before running local server for the first time, go to the root directory of your site and run
```bash
bundle
```

You may want to preview the site contents before publishing, so just run it by:
```bash
bundle exec jekyll s
```

## Resources
[quick tutorial](https://chirpy.cotes.page/)

[wiki](https://github.com/cotes2020/jekyll-theme-chirpy/wiki)
