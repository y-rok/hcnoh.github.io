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

이번 포스팅은 다음의 링크들을 참고하였다:
- [링크1](http://corej21.tistory.com/42)

## 경로 관련
- `home` 경로: `~`
  - 예제: `home`에다가 `temp`라는 이름의 디렉토리 생성

```bash
>>> mkdir ~/temp
```

- 바로 상위 경로: `..`
  - 예제: 현재 디렉토리의 상위 디렉토리로 이동

```bash
>>> cd ..
```

- 현재 경로: `.`
  - 예제: 현재 디렉토리에 `temp`라는 이름의 디렉토리 생성

```bash
>>> mkdir ./temp
```

## 파일/디렉토리 생성, 이동, 삭제
- 디렉토리 생성: `mkdir`
  - 예제: `dir_name`라는 이름의 디렉토리 생성

```bash
>>> mkdir dir_name
```

- 파일 및 디렉토리 삭제: `rm -rf`
  - 예제: `dir_name`라는 디렉토리와 하위 디렉토리 및 파일 전부 삭제

```bash
>>> rm -rf dir_name
```

- 파일 및 디렉토리 복사: `cp`
  - 옵션:
    - `-a`: 원본 파일의 속성, 링크 정보들을 그대로 유지하면서 복사
    - `-b`: 복사할 대상이 이미 있을 경우 기존 파일을 백업하고 복사
    - `-d`: 만약 복사할 원본이 심볼릭 링크일 때 심볼릭 자체를 복사
    - `-f`: 만약 복사할 대상이 이미 있으면 강제로 지우고 복사
    - `-i`: 만약 복사할 대상이 이미 있으면 사용자에게 물어
    - `-l`: 하드링크 형식으로 복사
    - `-P`: 원본 파일 지정을 경로와 같이했을 경우 그 경로 그대로 복사
    - `-p`: 파일의 소유자, 그룹, 권한, 시간 정보들이 그대로 보존되어 복사
    - `-r`: 원본이 파일이면 그냥 복사되고 디렉터리라면 디렉터리 전체가 복사
    - `-s`: 파일을 심볼릭 링크 형식으로 복사, 원본 파일이름을 절대 경로로 지정해야 함
    - `-u`: 복사할 대상이 있을 때 이 파일의 변경 날짜가 같거나 더 최근의 것이면 복사하지 않음
    - `-v`: 복사 상태를 보여줌
    - `-x`: 원본과 대상 파일의 파일시스템이 다를 경우에는 복사하지 않음
    - `-R`: 디렉터리를 복사할 경우 그 안에 포함된 모든 하위경로와 파일들을 모두 복사
  - 예제: 현재 위치에 있는 `dir_name`라는 디렉토리를 `home`으로 복사

```bash
>>> cp -r ./dir_name ~/dir_name
```

- 파일 및 디렉토리 이동 (또는 이름 변경): `mv`
  - 옵션:
    - `-b`: 이동 경로에 같은 이름의 파일이나 디렉터리가 존재하면 기존 파일을 백업한 뒤에 이동
    - `-f`: 이동 경로에 같은 이름의 파일이나 디렉터리가 존재하면 덮어쓸 때 묻지 않고 바로 덮어 씀
    - `-i`: 이동 경로에 같은 이름의 파일이나 디렉터리가 존재하면 덮어쓸 때 물어봄
    - `-v`: 이동 상태를 표시
  - 예제 `./temp`의 디렉토리를 `./temp_`으로 이름 변경

```bash
>>> mv ./temp ./temp_
```

## zip 압축 파일 관련
- zip 압축 풀기:

```bash
>>> unzip file_name.zip
```

- 특정 폴더로 zip 압축 풀기:

```bash
>>> unzip file_name.zip -d ./target
```

- 현재 폴더에 있는 내용 zip 압축 하기:

```bash
>>> zip test.zip ./*
```

- 하위 폴더까지 전부 압축:

```bash
>>> zip -r test.zip ./*
```
