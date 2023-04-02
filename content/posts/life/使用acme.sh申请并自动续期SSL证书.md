---
title: "使用acme.sh申请并自动续期SSL证书" #标题
date: 2023-03-15T20:52:43+08:00 #创建时间
lastmod: 2023-03-16T20:52:43+08:00 #更新时间
author: ["木木"] #作者
categories: 
- 日常
- 随笔
tags: 
- Daily
- Life
description: "" #描述
weight: # 输入1可以顶置文章，用来给文章展示排序，不填就默认按时间排序
slug: ""
draft: false # 是否为草稿
comments: false #是否展示评论
showToc: true # 显示目录
TocOpen: true # 自动展开目录
hidemeta: false # 是否隐藏文章的元信息，如发布日期、作者等
disableShare: true # 底部不显示分享栏
showbreadcrumbs: true #顶部显示当前路径
cover:
    image: "" #图片路径：
    caption: "" #图片底部描述
    alt: ""
    relative: false
---



## 一）ACME安装

```
curl  https://get.acme.sh | sh
```

安装程序会自动做以下操作：

- 自动把 acme.sh 安装到你的 **home** 的`.acme.sh`目录下，即`~/.acme.sh/`
- 自动创建一个 bash 的 alias, 方便你的使用: `alias acme.sh=~/.acme.sh/acme.sh`
- 自动为你创建 cronjob, 每天 0:00 点自动检测所有的证书, 如果快过期了, 需要更新, 则会自动更新证书.

## （二）更改默认证书机构

```
acme.sh --set-default-ca  --server  letsencrypt
```

acme被ZeroSSL收购，其默认的证书方式为ZeroSSL，但此证书生成时会携带邮箱，因此更换为letsencrypt。

当然，也可以在生成证书时加一个`--server`参数来决定生成什么证书

```
--server letsencrypt
```

## （三）生成证书

使用`acme.sh --issue`命令生成证书，但生成证书的同时会进行域名的所有权的验证。 **acme.sh** 有两种方式验证：http 和 dns 验证。

> 注意：如果需要生成泛域名（`*.a.com`）的证书，不能使用HTTP认证域名，需要改用DNS认证的方式

### DNS 验证方式（推荐,手动也可，但是作者不想手动.jpg）

需要在域名上添加一条 txt 解析记录, 验证域名所有权

##### 方式1：手动添加记录

a. 生成txt解析内容

```
acme.sh  --issue  --dns -d mydomain.com \
 --yes-I-know-dns-manual-mode-enough-go-ahead-please
```

> 以上mydomain.com只是测试域名，如果多个域名，则需多次使用-d配置，如`-d www.a.com -d img.a.com`

b. 把txt解析添加到域名管理面板中

c. 重新生成证书

```
acme.sh  --renew   -d mydomain.com \
  --yes-I-know-dns-manual-mode-enough-go-ahead-please
```

> 注意，重新生成使用的是`renew`参数，把生成txt解析内容命令的`issue`改为`renew`

##### 方式2：域名提供商api自动解析

> dns 方式的真正强大之处在于可以使用域名解析商提供的 api 自动添加 txt 记录完成验证.

a. 在域名提供商中，生成你的 api id 和 api key并记录

b. 引入api id和key，以dnspod为例

```
export DP_Id="1234"
export DP_Key="sADDsdasdgdsf"
```

不同提供商，API参数值各不同，可参考下面的表格：自动 DNS API 集成

c. 生成证书

```
acme.sh --issue --dns dns_dp  -d aa.com -d www.aa.com
```

`--dns`的配置值也是根据域名提供商来决定，dns_dp表示dnspod。更多参数值可看下方表格

表：自动 DNS API 集成

| 服务商名称   | 服务商简称 | 所需API参数                                                  | 获取API参数地址                                              |
| ------------ | ---------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| cloudxns     | cx         | `export CX_Key="123456"` `export CX_Secret="abcdef"`         | [点击访问](https://www.cloudxns.net/AccountManage/apimanage.html) |
| dnspod.cn    | dp         | `export DP_Id="123456"` `export DP_Key="abcdef"`             | [点击访问](https://www.dnspod.cn/console/user/security)      |
| aliyun       | ali        | `export Ali_Key="123456"` `export Ali_Secret="abcdef"`       | [点击访问](https://ak-console.aliyun.com/#/accesskey)        |
| cloudflare   | cf         | `export CF_Key="123456"` `export CF_Email="abc@example.com"` | [点击访问](https://dash.cloudflare.com/profile/api-tokens)   |
| linode       | linode     | `export LINODE_API_KEY="123456"`                             | [点击访问](https://manager.linode.com/profile/api)           |
| he           | he         | `export HE_Username="username"` `export HE_Password="password"` | [he](https://dns.he.net/)的用户名密码                        |
| digitalocean | dgon       | `export DO_API_KEY="123456"`                                 | [点击访问](https://cloud.digitalocean.com/settings/applications) |
| namesilo     | namesilo   | `export Namesilo_Key="123456"`                               | [点击访问](https://www.namesilo.com/account_api.php)         |
| aws          | aws        | `export AWS_ACCESS_KEY_ID=123456` `export AWS_SECRET_ACCESS_KEY=abcdef` | [点击访问](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html) |
| namecom      | namecom    | `export Namecom_Username="username"` `export Namecom_Token="123456"` | [点击访问](https://www.name.com/reseller/apply)              |
| freedns      | freedns    | `export FREEDNS_User="username"` `export FREEDNS_Password="password"` | [freedns](https://freedns.afraid.org/)的用户名密码           |
| godaddy      | gd         | `export GD_Key="123456"` `export GD_Secret="abcdef"`         | [点击访问](https://developer.godaddy.com/keys/)              |
| yandex       | yandex     | `export PDD_Token="abcdef"`                                  | [点击访问](https://tech.yandex.com/domain/doc/concepts/access-docpage/) |

更多dnsapi的使用，可以查看[文档](https://github.com/acmesh-official/acme.sh/wiki/dnsapi)

## （四）copy/安装 证书

默认生成的证书都放在安装目录下: `~/.acme.sh/`，但是不要在web服务器中直接引用目录下的证书文件，也不要手动来拷贝证书文件到具体的web服务器中，手动拷贝会导致之后更新证书流程不能完全自动。

正确方式是使用acme.sh的安装证书命令，acme.sh自动拷贝证书文件到具体目录中，拷贝命令会被记录下来，之后自动更新证书流程也会执行此拷贝步骤，从而实现更新证书流程的完全自动化。

格式例子如下：

```
acme.sh --install-cert -d xxx \
		--cert-file xxx \
		--key-file xxx \
		--fullchain-file xxx\
		--reloadcmd xxx
```

根据web服务器需要的文件按需引入对应的参数，reloadcmd定义证书更新后重启对应的web服务命令。

以nginx为例：

```
acme.sh --install-cert -d www.a.com -d img.a.com \
		--key-file   /etc/nginx/cert_file/key.pem  \
		--fullchain-file /etc/nginx/cert_file/fullchain.pem \
		--reloadcmd     "service nginx force-reload"
```

## （五）web服务使用证书

通过上一步安装证书，已经把证书拷贝到目标的目录，接下来就是在web服务中使用证书即可。

以nginx为例：

```
...
server {
  listen       443 ssl;
  ssl_certificate      /etc/nginx/cert_file/fullchain.pem;
  ssl_certificate_key  /etc/nginx/cert_file/key.pem;
  # ...
}
```

## 更新证书

目前证书在 60 天以后会自动更新，你无需任何操作，因为在acme.sh安装时，已经把相关的自动更新程序写入到crontab中，如果想要查看，可以通过以下命令：

```
crontab -l
```

输出内容包含一个自动更新程序，大致内容如下：

```
56 * * * * "/root/.acme.sh"/acme.sh --cron --home "/root/.acme.sh" > /dev/null
```

## 停止自动更新

```
acme.sh --remove -d example.com 
```

或者手动在`~/.acme.sh/`目录下删除对应的域名目录，如`~/.acme.sh/a.com`。
