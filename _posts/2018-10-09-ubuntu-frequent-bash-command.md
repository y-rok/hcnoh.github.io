---
layout: post
title: "Ubuntu 자주 사용하는 bash 명령어 정리"
date: 2018-10-09 21:45:48
tagline: "Ubuntu 16.04에서 작업 도중에 자주 사용되는 bash 명령어를 정리"
categories:
- Ubuntu 16.04
tags:
- linux
image: /thumbnail-mobile.png
author: "Hyungcheol Noh"
permalink: /2018-10-09-ubuntu-frequent-bash-command
---

## 경로 관련
- home 경로:

```bash
>>> ~
```

- 바로 상위 경로:

```bash
>>> ..
```

- 현재 경로:

```bash
>>> .
```

## 압축 파일 관련
- zip 압축 풀기:

```bash
>>> unzip file_name.zip
```

- 특정 폴더로 zip 압축 풀기:

```bash
unzip file_name.zip -d ./target
```

- 현재 폴더에 있는 내용 zip 압축 하기:

```bash
zip test.zip ./*
```

- 하위 폴더까지 전부 압축:

```bash
zip -r test.zip ./*
```