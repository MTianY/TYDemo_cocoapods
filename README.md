# cocoapods

### 常用命令

- 查看当前`cocoapods`版本

```zsh
pod --version
```

- 查看本地索引库

```zsh
// 查看本地索引库
pod repo

master
- Type: git (master)
- URL:  https://github.com/CocoaPods/Specs.git
- Path: /Users/Maty/.cocoapods/repos/master

1 repo

// 1.上面本地只有一个索引库, 就是官方的 master 索引库
// 2.URL 为远程的 url 地址.
// 3.Path 为从远程的 url 地址 clone 到本地存储的地方
```

### 发布框架步骤

- 本地写好要发布的框架
- github 创建好仓库,然后 clone 到本地
- 将本地的框架放到仓库中,然后提交
- 打 tag
- 然后写一个 `podspec`文件来描述这个框架. 执行命令

```zsh
pod spec create 文件名(最好同框架名)
```

- 然后打开 `.podspec` 文件

```objc
...

// 项目名
s.name         = "TYDemo_cocoapods"
// 版本
s.version      = "0.0.1"
// 项目的简要描述
s.summary      = "cocoapods test Demo"
// 项目的详细描述(描述文字最好比上面的多一些,防止报警告)
s.description  = <<-DESC
"a demo for cocoapods, very nb...."
                   DESC
// 项目所在地址
s.homepage     = "https://github.com/MTianY/TYDemo_cocoapods"
// 协议  
s.license      = "Apache License, Version 2.0"
// 作者信息
s.author             = { "Maty" => "mtystar@qq.com" }
// 仓库地址, tag 指定的 version, 这里不用改动,只需要改动上面的 version 就好了
s.source       = { :git => "s.source       = { :git => "https://github.com/MTianY/TYDemo_cocoapods.git", :tag => "#{s.version}" }", :tag => "#{s.version}" }

// 别人 pod install 这个项目时引用的工程路径.(把需要的给别人引用)
// "Classes/**/*.{h,m}" 中的"**"表示匹配所有的目录
// s.source_files  = "Classes", "Classes/**/*.{h,m}"
// s.exclude_files = "Classes/Exclude"

s.source_files = "TYTestAPI", "TYDemo_cocoapods/TYTestCocoapods/TYTestAPI/**/*.{h,m}"

// 是不是 arc 环境
s.requires_arc = true
```

- 保存 spec 文件, 然后提交

```git
git status
git add .
git commit -m "提交 .podspec文件"
git push
```

- 将整个 podspec 文件上传到远程的官方 pod 索引库中去
- 首先先进行远程验证(直接跳过本地验证,因为要提交的话就会经过远程验证,所以直接走远程验证)
    - 验证语法
    - 验证地址
    - 验证文件能否被匹配到 

```pod
pod spec lint
```

- 提交

```pod
pod trunk register mtystar@qq.com 'Maty' --verbose
```

- 然后登陆邮箱拷贝地址然后打开一下
- 成功之后执行如下命令

```pod
pod trunk push 仓库名
```


