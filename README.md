# Accesser 中国电信贵阳贵安定制版

一个 [Accesser](https://github.com/URenko/Accesser) 分支，用于解决 SNI RST 导致维基百科、Pixiv 等与邪教、色情无关联的境外站点和部分中国电信贵阳贵安校园网络**间歇性乱阻断，但是内容正常**的站点无法访问的问题。

[![](https://img.shields.io/github/release/Diamochang/AccesserCTC.svg)](https://github.com/Diamochang/AccesserCTC/releases/latest)
[![](https://img.shields.io/github/license/Diamochang/AccesserCTC.svg)](https://github.com/Diamochang/AccesserCTC/blob/master/LICENSE)

## 使用

以下内容从原版 README 复制而来，只移除了后面的开发时间线并修改部分链接。这些内容中有关 PIP 的部分**暂不适用于此定制版本**。

### 如果不知道什么是Python
从[这里](https://github.com/Diamochang/AccesserCTC/releases/download/latest/accesser-ctc-gyg.exe)下载Windows一键程序，运行既可（建议关闭其他代理软件），首次使用会要求安装证书，选是即可。
### 如果已经安装了Python 3.10*或更高版本
```
pip3 install -U "accesser[doh,doq]"
```
如果你不需要 DNS-over-HTTPS 和 DNS-over-QUIC，则可以不用带`[doh,doq]`。

然后通过如下命令启动：
```
accesser
```
对于Windows系统，默认情况下（没有指定`--notsetproxy`）会设置PAC代理为`http://localhost:7654/pac/?t=<随机数>`，如果没有可以手动设置。

此外，对于Windows系统，默认情况下（没有指定`--notimportca`）会自动导入证书至系统，如果没有可以手动导入，请看[这里](https://github.com/URenko/Accesser/wiki/FAQ#q-windows%E8%AE%BF%E9%97%AE%E7%9B%B8%E5%85%B3%E7%BD%91%E7%AB%99%E5%87%BA%E7%8E%B0%E8%AF%81%E4%B9%A6%E9%94%99%E8%AF%AF%E6%82%A8%E7%9A%84%E8%BF%9E%E6%8E%A5%E4%B8%8D%E6%98%AF%E7%A7%81%E5%AF%86%E8%BF%9E%E6%8E%A5neterr_cert_invalid%E4%B9%8B%E7%B1%BB%E7%9A%84%E6%80%8E%E4%B9%88%E5%8A%9E%E8%AF%81%E4%B9%A6%E5%AF%BC%E5%85%A5%E9%94%99%E8%AF%AF%E6%80%8E%E4%B9%88%E5%8A%9E%E5%A6%82%E4%BD%95%E5%8D%B8%E8%BD%BD%E8%AF%81%E4%B9%A6)（根证书可从`http://localhost:7654/CERT/root.crt`获取）。

*可以使用例如[pyenv](https://github.com/pyenv/pyenv)来安装所需的Python版本（推荐Python 3.11+）。

## 设置
启动一次Accesser后，会在 **工作目录** 下生成`config.toml` 和 `rules.toml`，具体含义见其中注释，保存后重新打开程序。

## 进阶1: 与v2ray等其他代理软件一起使用
Accesser是一个本地HTTP代理，默认代理地址为`http://localhost:7654`，只要网络流量能从其他代理软件以HTTP代理导出就能联合使用。

以[v2ray](https://github.com/v2fly/v2ray-core)为例，可以添加一个HTTP的outbound指向`http://localhost:7654`，并设置相应的路由规则，将维基百科、Pixiv等站点的流量送到这个outbound。
并在启动 Accesser 时带上 `--notsetproxy` 参数以避免 Accesser 设置系统代理。

此外，你还可以设置一个DNS outbound，然后编辑`config.toml`让Accesser使用这一DNS。

## 进阶2: 增加支持的网站
编辑工作目录下的pac文件（如果是一键程序，可以从GitHub下载这一文件到工作目录），使要支持的网站从代理过。

然而，并不是所有站点都可以直接工作，可能需要一些调节，见[如何适配站点](https://github.com/URenko/Accesser/wiki/如何适配站点)。
