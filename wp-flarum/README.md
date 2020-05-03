大概说说功能：

Single Sign On 可以把 flarum 上面那些注册，登陆，退出 链接统统改成 wordpress 的，并且隐藏掉 flarum 里的修改个人资料，忘记密码 等模块。

开启后，flarum 的登陆、注册、登出就只在会 wordpress 完成，用户登录时会同时写入 flarum 的 cookie，如果 flarum 里没有该用户，就会自动给注册一个然后写入 cookie。新用户注册时会在 wordpress 和 flarum 同时注册，然后登录，功能还是比较完善了。

安装分两部分：

wordpress 部分
1.进入 flarum 数据库的表 api_keys， 填入一个随机的 token（可以去百度找个随机密码生成后填入）
2.下载 Single Sign On 的源码，把 sample-website 目录里的 config.php.dist 改名为 config.php
3.修改 config.php 里面的设置，flarum_api_key 是第1步生成的 token，password_token 你自己写个（他会是自动注册用户名时使用的加密密匙）
4.上传整个 sample-website 目录到 wordpress 的插件目录，然后启动该插件。

flarum 部分
1.使用 composer require wuethrich44/flarum-ext-sso 安装插件
2.后台启用插件后，填入3个地址
注册链接: http://example.com/wp-login.php?action=register
登录链接: http://example.com/wp-login.php?redirect_to=forum
注销链接: http://example.com/wp-login.php?action=logout

3.然后清空掉浏览器的所有缓存试试吧。

还有些小问题：
1.flarum 如果已经有这个用户，则自动注册失败，而且该用户将无法登陆。
2.flarum 登录后返回论坛的功能会跟一些插件冲突。
3.点击 flarum 的退出后，会进入 wordpress 的退出确认页面，如果这时候拒绝登出，事实上 flarum 已经被登出了。