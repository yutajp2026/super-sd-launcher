# おすすめソフト
これらのアプリには様々な機能が備わっており、本ソフトで使用したモデルを流用できるものもあります。右上のOutline(三本線)から全体を確認できます。
# アプリあり
## [InvokeAI](https://invoke.ai/start-here/installation/)
最も使いやすく、本ソフトとのモデルの共有もしやすいです。
### モデル流用
`元位置でインストール`にチェックをつけてモデルパスに入力
## [ComfyUI](https://comfy.org/download) 
アプリ版ですが、ワークフローなどの知識が必要です。
### モデル流用
Models内のdiffusion_modelsに移動またはコピー
# ワンクリックインストール
## [SwarmUI](https://swarmui.net/)
ワンクリックインストールなうえWindowsはデスクトップから起動できるので使いやすいです。
### インストール時の注意点
- インストーラはインストールしたい場所に置きます。
- GUIとして動作させたい場合は[.NET SDK 10.0](https://dotnet.microsoft.com/ja-jp/download/dotnet/10.0)が必要です。
### モデル流用
Models内のStable-Diffusionに移動またはコピー
## [SD.Next](https://vladmandic.github.io/sdnext-docs/)
Windowsのみランチャー版があります。
### Windowsランチャーでのインストール時の注意点
- ランチャーのダウンロードと初回起動でセキュリティに引っ掛かります。
- インストールするディレクトリは初期値がランチャーの場所になっていますが、オプションで編集できます。
### モデル流用
Models内のStable-Diffusionに移動またはコピー
# コードのみ
## [stable-diffusion-webui](https://github.com/AUTOMATIC1111/stable-diffusion-webui)
アプリの容量が比較的小さく(本ソフトよりは大きい)、WebUIは使いやすいです。しかし公式の説明通りにインストールしようとすると必ず詰むので独自にインストール方法を説明します。
### Windowsへのインストール
1. [Python3.10.6](https://www.python.org/downloads/release/python-3106/)をインストール(ほかのバージョンがある場合は環境変数にパスを追加しないことをおすすめします)
2. [VC Redist](https://learn.microsoft.com/ja-jp/cpp/windows/latest-supported-vc-redist?view=msvc-170)がない場合はインストール
3. コマンドプロンプトを開き`winget install --id Git.Git -e --source winget`コマンドでgitをインストール
4. `git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git`コマンドでリポジトリをクローン
5. `webui-user.bat`の内容をメモ帳で下記に変更(remコマンドはないほうがよい)
```
@echo off
rem 下記はPythonインストーラでの初期パス(必要に応じて変更または削除)。
rem 他のバージョンのPythonを使わないようにするために記載しています。
set PYTHON="C:\Users\%username%\AppData\Local\Programs\Python\Python310\python.exe"

nvidia-smi
if not %errorlevel% == 0 (
    set COMMANDLINE_ARGS="--use-cpu all --precision full --no-half --skip-torch-cuda-test"
)

set STABLE_DIFFUSION_REPO=https://github.com/w-e-w/stablediffusion.git
set CLIP_PACKAGE=git+https://github.com/openai/CLIP.git

call webui.bat
```
6. `webui-user.bat`(起動ファイル)を実行
### Linuxへのインストール
1. 下記コマンドで依存関係をインストール
```bash
# Debian系(Ubuntuなど)
sudo apt install wget git libgl1 libglib2.0-0
```
```bash
# Arch系
sudo pacman -S wget git
```
2. 下記コマンドでPython3.11.16をインストール
```bash
# Debian系(Ubuntuなど)
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt update
sudo apt install python3.11 python3.11-venv
```
```bash
# Arch系
sudo pacman -S yay
yay -S python311
```
3. `git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git`コマンドでリポジトリをクローン
4. `webui-user.sh`の内容を下記に変更
```bash
#!/bin/bash

python_cmd="python3.11"

if command -v nvidia-smi >/dev/null 2>&1 && nvidia-smi >/dev/null 2>&1; then
    echo "GPU is available"
else
    export COMMANDLINE_ARGS="--use-cpu all --precision full --no-half --skip-torch-cuda-test"
fi

export STABLE_DIFFUSION_REPO=https://github.com/w-e-w/stablediffusion.git
export CLIP_PACKAGE=git+https://github.com/openai/CLIP.git
```
5. `webui.sh`(起動ファイル)を実行
### モデル流用
Models内のStable-Diffusionに移動またはコピー(ただし本ソフトと同じモデルが自動ダウンロードされます)
## [FastSDCPU](https://github.com/rupeshs/fastsdcpu)
CPUだけで速く画像を生成でき、起動方法がさまざまです(おすすめはGUI)。
### インストール時の注意点
Pythonと[UV](https://docs.astral.sh/uv/)が必要です。
### モデル流用
1. configs\stable-diffusion-modelsにパスを入力
2. 起動してLCM-Loraを有効化
3. LCM-Loraベースモデルを選択
