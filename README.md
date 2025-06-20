![logo-blue](https://user-images.githubusercontent.com/51039935/197520391-f35db354-6071-4c12-86ea-fc450f04bc85.png)
# NAS媒体库资源归集、整理自动化工具

[![GitHub stars](https://img.shields.io/github/stars/hsuyelin/nas-tools?style=plastic)](https://github.com/hsuyelin/nas-tools/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/hsuyelin/nas-tools?style=plastic)](https://github.com/hsuyelin/nas-tools/network/members)
[![GitHub issues](https://img.shields.io/github/issues/hsuyelin/nas-tools?style=plastic)](https://github.com/hsuyelin/nas-tools/issues)
[![GitHub license](https://img.shields.io/github/license/hsuyelin/nas-tools?style=plastic)](https://github.com/hsuyelin/nas-tools/blob/master/LICENSE.md)
[![Docker pulls](https://img.shields.io/docker/pulls/hsuyelin/nas-tools?style=plastic)](https://hub.docker.com/r/hsuyelin/nas-tools)
[![Platform](https://img.shields.io/badge/platform-amd64/arm64-pink?style=plastic)](https://hub.docker.com/r/hsuyelin/nas-tools)

## zp29维护声明

1）本维护项目为[nas-tools](https://github.com/NAStool/nas-tools)维护项目非官方项目；  
2）本维护项目旨在帮助喜欢PT的小伙伴更加易用，本人未创建任何交流群或频道；  
3）本维护项目提交的修复和需求皆为开源，任何维护该项目的小伙伴皆可参考，但尽量注明出处；  
4）使用本维护项目请尽量保持低调，尽可能不在交流群或者频道传播，自己使用即可；  
5）欢迎任何形式的pr，请尽量将pr内容描述清楚；  

## 开发路线及官方原版新增内容

基于官方 2.9.1 版本

[开发路线](https://github.com/hsuyelin/nas-tools/discussions/91)

- [x] 联动CMS使用115下载

## 安装
### 1、Docker
```
docker pull zp29/nas-tools:latest
```

### 2、本地Docker运行
仅支持python3.10版本，需要预安装cython（python3 -m pip install Cython），如发现缺少依赖包需额外安装：
```
git clone -b master https://github.com/zp29/zp29/nas-tools-291-cms --recurse-submodule 
cd nas-tools-291-cms
docker build -t zp29/nas-tools:latest -f docker/Dockerfile .
docker-compose up -d
```


## 官方免责

1）本软件仅供学习交流使用，对用户的行为及内容毫不知情，使用本软件产生的任何责任需由使用者本人承担。  
2）本软件代码开源，基于开源代码进行修改，人为去除相关限制导致软件被分发、传播并造成责任事件的，需由代码修改发布者承担全部责任，不建议对用户认证机制进行规避或修改并公开发布。  
3）本项目没有在任何地方发布捐赠信息页面，也不会接受捐赠或收费，请仔细辨别避免误导。


更多功能使用请查看 [nas-tools wiki](https://t.me/NAStool_wiki)
