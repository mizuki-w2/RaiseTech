## VPCの作成
![01](lecture04-image/01.png)

## EC2
![02](lecture04-image/02.png)
![03](03.png/03.png)


## RDS
![05](lecture04-image/05.png)

## セキュリティ設定
### EC2
![04](lecture04-image/04.png)　　
sshに接続できるようにポート範囲を22に設定。　　

### RDS
![06](lecture04-image/06.png)
![07](lecture04-image/07.png)
EC2からRDSへ接続できるようにインバウンドはEC2のセキュリティグループを設定。　　

EC2、RDSのアウトバウンドは全て許可に設定。
## EC2からRDSへ接続
![08](lecture04-image/08.png)
teratermを利用。　　

ログイン時はファイルに保存したキーペアを使う。　　

`sudo yum install mysql`でMySQLをインストール。　　

`mysql -h (RDSのエンドポイント）-u (マスターユーザー名) -p (マスターパスワード)`を入力し、接続できることを確認。　　  


## 感想
EC2からRDSへの接続ができず、苦戦したおかげでだんだんとセキュリティ設定と接続のイメージが出来るようになった。　　
とはいえ完全な理解は難しく、ここはもう少し時間をかけて勉強したい。   

コマンドミスや設定の見落としがあり、ひとつひとつ検証していく必要がある。
