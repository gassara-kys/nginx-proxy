# nginx-proxy

nginxのリバプロサンプル

## やりたいこと

- SSL/TLSの暗号化通信の終端を担う
- HTTPSを強制する
- VirtualHostの設定をしてバックエンドのホストへ転送する

## 準備

- dockerのインストール
- 証明書ファイル（サンプルはオレオレ証明書）

## ビルドと起動

- ビルド＆起動

```bash
$ docker build -t nginx-proxy:latest .
$ docker run -d -p 80:80 -p 443:443 --name nginx-proxy nginx-proxy:latest
```

- ブラウザやcurlで確認

```
http://{server_name}/
https://{server_name}/
```

## カスタマイズ

- VirtualHostの設定
  - 例えば新たにぶら下げるサイトを追加する場合は、 `nginx-proxy/conf.d/hogehoge.com.conf` のようなファイルを作成し、そこにVirtualHost設定をしていくことを想定しています。
  - `nginx-proxy/conf.d/default.conf` を流用して作成できます
  - `.gitignore` で `*.*.conf` のファイルはコミット対象外にしています（セキュリティ観点でリポジトリにコミットできない情報が含まれるものはその形式にする）
- 正規の証明書の入れ替え
- ディレクトリ構成

```
nginx-proxy/
    \_ conf.d/
        \_ *.cnof      # 各種VirtualHostを設定（複数可） 
        \_ server.crt  # 証明書関連
        \_ server.csr
        \_ server.key
```

