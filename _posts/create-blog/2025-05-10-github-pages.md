---
title: 用Github Pages + Jekyll搭建你的专属博客
date: 2025-05-10
categories: [博客搭建]
tags: [博客搭建]
---

> 欢迎参考最终成果：[https://rendeyuwei.github.io/](https://rendeyuwei.github.io/)  
> GitHub地址：[https://github.com/rendeyuwei/rendeyuwei.github.io](https://github.com/rendeyuwei/rendeyuwei.github.io) 如有问题欢迎在github上提问
{: .prompt-info }

GitHub Pages 是通过 GitHub 托管和发布的公共网页。除此之外，我们还需要借助[Jekyll](https://jekyllrb.com/)主体来美化我们的博客。

在Jekyll你可以手动安装来采用自定义主题，但在这里我们直接通过社区主题的启动器来创建一个项目，如果你只想聚焦于编写博客上，而不是折腾Jekyll的话。

我选择了这个博客主题作为我的主题，本篇博客也以这个为例子：[https://chirpy.cotes.page/posts/getting-started/](https://chirpy.cotes.page/posts/getting-started/)
当然你可以在这里找到更多的主题：[https://github.com/topics/jekyll-theme](https://github.com/topics/jekyll-theme)

## 创建仓库
1. 首先登陆了github之后，进入这个博客主题的启动器：[https://github.com/cotes2020/chirpy-starter](https://github.com/cotes2020/chirpy-starter) 然后点击Use this template，并create
![](assets/img/create-blog/image copy 13.png)
1. 输入`username.github.io`作为存储库的名称，username替换成你自己想命名的名称。
![](assets/img/create-blog/image copy 14.png)
1. 然后创建完成

## 安装Jekyll
以下的教程以mac系统为例，其他系统安装可参考文档，类似。
1. 安装依赖
Jekyll有一些依赖需要安装：
- [Ruby](https://www.ruby-lang.org/en/downloads/) version **2.7.0** or higher, including all development headers (check your Ruby version using `ruby -v`)
- [RubyGems](https://rubygems.org/pages/download) (check your Gems version using `gem -v`)
- [GCC](https://gcc.gnu.org/install/) and [Make](https://www.gnu.org/software/make/) (check versions using `gcc -v`,`g++ -v`, and `make -v`)
这几个依赖的安装可以参考官方文档：[https://jekyllrb.com/docs/installation/macos/](https://jekyllrb.com/docs/installation/macos/)

注意，关于Ruby的安装，mac上本身带有ruby，但是版本较低，如果安装官方文档安装会报错，可以参考我的安装方式：
1. 使用 homebrew 安装 rbenv，ruby-build
```
  brew install rbenv ruby-build
```
2. 配置环境变量，把这些加入到`~/.zshrc`中
```
export PATH="$HOME/.rbenv/bin:$PATH" 
eval "$(rbenv init -)"
```
 3. 安装 ruby
查看可用 ruby 版本，我这里安装了最新的3.4.2版本
```
rbenv install --list

rbenv install 3.4.2

rbenv global 3.4.2

ruby -v
```
ruby -v成功输出3.4.2版本
我的其他依赖系统本身就有，如果没有可以参考上面给出的文档来安装。

2. 安装Jekyll
```
gem install jekyll bundler
```

## 启动博客
回到我们刚才创建的博客，clone到本地之后，命令行执行以下两行
```
bundle install

bundle exec jekyll s
```
可以看到博客就启动在了本地服务，http://127.0.0.1:4000/，然后就可查看模版的效果

然后需要对默认博客模板进行配置，在_config.yml文件里，包括以下四个属性，关于配置的参考，可以看[官方的解释](https://chirpy.cotes.page/posts/getting-started/)：
- `url` 这里配置https://username.github.io，就是你创建项目的名字
- `avatar` 这里配置头像
- `timezone` 这里配置时区 Asia/Shanghai
- `lang` 这里配置语言 zh-CN

然后回到项目设置里，将这个更改：
![](assets/img/create-blog/image copy 15.png)

记得将你的仓库设置成public进入设置，选择Github Pages从哪个分支来构建，我这里默认选择main分支的根文件
![](assets/img/create-blog/image copy 16.png)

然后将代码提交至远程仓库，GitHub就会自动构建了，如果构建过程中报错找不到对应的`assets`文件，记得将[https://github.com/cotes2020/jekyll-theme-chirpy/tree/master/assets](https://github.com/cotes2020/jekyll-theme-chirpy/tree/master/assets)里`assets`的文件复制到你的项目里

## 提交文档
1. （可选）你可以对你的默认main分支进行保护，防止有人随意在上面进行提交：
![](assets/img/create-blog/image copy 17.png)
在Rules里面的Rulesets里面新建一条，因为我已经建好了，所以里面有一个，
在这里面，我创建的规则是，对于默认的Default分支，限制了以下的规则，你可以根据自己情况来选择

以下是Gemini AI对于配置的方法描述：
> 在 GitHub 上，限制直接向 main（或 master）分支提交代码是一种常见的最佳实践，它可以有效地维护代码库的稳定性和质量。通过强制使用 Pull Request（PR）流程，可以确保所有更改都经过代码审查和测试，然后再合并到主分支。以下是如何在 GitHub 上设置这种限制的几种方法：
> 
> **1. 使用分支保护规则：**
> 
> 这是最常用的方法，它允许你配置各种规则来保护你的分支。以下是如何操作：
> 
> - **进入仓库设置：** 在你的 GitHub 仓库页面，点击 “Settings”（设置）。
> - **导航到分支设置：** 在左侧边栏的 “Code and automation”（代码和自动化）部分，点击 “Branches”（分支）。
> - **添加分支保护规则：** 在 “Branch protection rules”（分支保护规则）部分，点击 “Add rule”（添加规则）。
> - **指定要保护的分支：** 在 “Branch name pattern”（分支名称模式）下，输入 `main`（或 `master`，取决于你的主分支名称）。
> - **配置规则：**
>     - **Require pull requests before merging（合并前需要拉取请求）：** 勾选此项以强制使用 PR 流程。你可以设置需要的最少审查人数。
>     - **Require status checks to pass before merging（合并前需要通过状态检查）：** 如果你使用了 CI/CD（持续集成/持续交付）工具，勾选此项以确保所有测试都通过。
>     - **Require conversation resolution before merging（合并前需要解决所有对话）：** 勾选此项以确保所有代码审查的评论都已解决。
>     - 其他选项，如 “Include administrators”（包含管理员）和 “Allow force pushes”（允许强制推送），根据你的需要进行配置。通常不建议允许强制推送到受保护的分支。
> - **保存更改：** 点击 “Save changes”（保存更改）。

2. 接下来创建一个分支（有很多种办法），然后本地clone了之后，在新分支上提交文档，最终在Pull request里面提交合并的请求即可

3. 接下来就可以进行文章创作，在根目录下的_posts文件夹下面创建你的md文件，然后提交上去就可以啦，记住文件名要以`YYYY-MM-DD-name.md` 的格式来命名

4. push上去之后，github actions会自动部署，然后你就可以看到你的文章啦

