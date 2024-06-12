
# Pyinstaller ?
- pyinstaller는 python 앱과 모든 dependency들을 하나의 패키지로 묶어주는 라이브러리다.
- python 인터프리터나 모듈을 설치하지않고도 패키지된 앱을 실행할 수 있게 해준다.
- python 3.8부터 지원된다.

## Pyinstaller 사용 이유
배포를 쉽게하기 위하여

## install
```
# pip install pyinstaller
```
- https://pyinstaller.org/en/stable/

## simple usage
```
# pyinstaller --onefile main.py
```
  - --onefile 옵션은 단일 exe 파일로 생성하라는 의미
- ./dist dir에 실행파일이 생성되고 ./에 main.spec 파일이 생김


# pyi-makespec
- pyinstaller가 실행될때 수행할 작업에 대한 설명이 된 파일을 만드는 명령어
- pyi-makesepc은 pyinstaller에게 기본 실행파일과 동적 라이브러리가 포함된 배포디렉터리를 생성하도록 지시하는 spec file을 생성한다.
- https://pyinstaller.org/en/stable/man/pyi-makespec.html

## simple usage
```
# pyi-makespec [--onefile] --name TestSpec yourprogram.py
# pyinstaller TestSpec.spec
```
## pyi-makespec options
- --name: spec file에 할당할 이름
- --paths: imports를 가져오기위한 경로 설정
- --additional-hooks-dir: hooks를 가져오기위한 추가 경로 설정
- --hidden-import: 소스코드에 사용되지않은 import를 가져옴

## pyinstaller hooks github
- https://github.com/pyinstaller/pyinstaller-hooks-contrib

## spec file example
```python
# -*- mode: python ; coding: utf-8 -*-
a = Analysis(
    ['yourprogram.py'],
    pathex=['./'],
    binaries=[],
    datas=[],
    hiddenimports=[],
    hookspath=[],
    hooksconfig={},
    runtime_hooks=[],
    excludes=[],
    noarchive=False,
    optimize=0,
)
pyz = PYZ(a.pure)

exe = EXE(
    pyz,
    a.scripts,
    [],
    exclude_binaries=True,
    name='TestSpec',
    debug=False,
    bootloader_ignore_signals=False,
    strip=False,
    upx=True,
    console=True,
    disable_windowed_traceback=False,
    argv_emulation=False,
    target_arch=None,
    codesign_identity=None,
    entitlements_file=None,
)
coll = COLLECT(
    exe,
    a.binaries,
    a.datas,
    strip=False,
    upx=True,
    upx_exclude=[],
    name='BFC',
)
```


# pyarmor
- python 코드를 난독화해주는 라이브러리

## usage
```
# pyarmor register regfild.zip
# pyarmor register
# pyarmor pack -s TestSpec.spec yourprogram.py
```
- pyarmor pack: pyarmor를 사용하여 패키징 작업을 수행한다.
- -s: 지정한 파일을 사용하여 패키징 작업을 수행한다.
- --clean: 패키징을 시작하기 전에 이전에 생성된 임시 파일이나 빌드 파일을 모두 삭제하라는 의미
- yourprogram.py: 보호 및 패키징할 메인 python 스크립트
