### 課題
1. アプリケーションの起動
2. APサーバーの名前とバージョンを確認
3. APサーバー終了後の確認
4. DBサーバーの名前とバージョンを確認
5. DBサーバー終了後の確認


1.アプリケーションの確認  

![AP起動](https://1drv.ms/i/c/e776efc90acd7ea5/ET3ntF-o9mdChtoREQRphkYBHOrU5No71NpGxa5uShH6Bg?e=ucZC7p)  
![AP起動ブラウザ](https://1drv.ms/i/c/e776efc90acd7ea5/EdEMl41wIepMjMEBZr0erUQBGhFvIlr_aZB7rReUztM83Q?e=2OQLNE)  
bin/cloud9_devでアプリケーション起動。

2.APサーバーの名前とバージョンを確認  
![APサーバー確認](https://1drv.ms/i/c/e776efc90acd7ea5/EZ9KvOZp4E5PkiBhVWFAS9YBK5aHBAeS8ri-yFDD4V21IQ?e=ijvDzo)   
Pumaのバージョン確認。


3.APサーバー終了後の確認  
![APサーバー終了](https://1drv.ms/i/c/e776efc90acd7ea5/EQknfA2TtWdEqHIBNQgwNTgBuIRgdGoKsDT6sox9x0DQPw?e=751eXT)    
rails sで起動。CTRL+CキーでPuma停止。 アプリは起動できず、エラーになる。 

4.DBサーバーの名前とバージョンを確認  
![DBバージョン](https://1drv.ms/i/c/e776efc90acd7ea5/EVCS8ug7IM9Al5meAKMtLNgBP6K8iFZDjAz6ZtyG68Xhqw?e=xcsHqM)   
mysql --versionコマンド。


5.DBサーバ終了後の確認  
![DBサーバー終了](https://1drv.ms/i/c/e776efc90acd7ea5/ET7fFRJF9IxJscCaHPJKrBABP22va7--EkXdMNifAGN9oQ?e=dbU3mm)  
sudo service mysqld stopで停止。エラーが表示される。

### 感想
エラーの対処法がなかなか見つからず、かなり苦戦した。  
Linuxコマンドの理解を深めていくうちに今どこのファイルにいるのか、何をしているのかが少しずつ分かるようになった。  
まだ曖昧な部分があるし、合っているのか不安な部分はたくさんあるので、もっと深いところまで突き詰めていけるよう頑張りたい。
