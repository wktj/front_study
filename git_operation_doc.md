> git config --global user.name "wktj"	#配置用户名（与github设置的用户名保持一致）
>
> git config --global user.email "2276689820@qq.com"   #配置邮箱信息（与github设置的邮箱保持一致）

获取ssh密钥，实现本地连接github

> ssh keygen -t rsa -C "github上注册使用的邮箱"
>
> 连按三次enter键获得密钥的本地保存地址
>
> 复制密钥内容到github上sitting进行配置

绑定ssh连接

> git bash 界面 
> ssh -T git@github.com 命令执行后即可绑定

克隆远程仓库

> git clone "hub主页链接"

提交远程仓库需要两步

> git add .  或者固定的文件名 git add test.txt    将修改或新建的文件存入git暂缓区
> git commit -m "描述" 提交到本地仓库，并以参数-m添加对应描述
>
> git push origin main 提交远程仓库