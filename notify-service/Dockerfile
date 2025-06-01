# ベースイメージとしてPythonを使用
FROM python:3.12-slim

# 作業ディレクトリを設定
WORKDIR /app

# 必要なファイルをコピー
COPY requirements.txt requirements.txt
COPY notify-service.py notify-service.py

# ライブラリをインストール
RUN pip install -r requirements.txt

# アプリケーションを起動
CMD ["python", "notify-service.py"]
