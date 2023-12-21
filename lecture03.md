### 第３回課題提出  

- サンプルアプリケーションのデプロイ
- APサーバーについて調べる
- DBサーバについて調べる

  
### 取り組んだこと、学んだこと

Rubyのバージョン確認`ruby -v`  
`rvm install 3.1.2`でインストール  
`rvm use 3.1.2`でバージョンの変更 もう一度`ruby -v`で指定したバージョンであることを確認  

#### DBサーバーの環境構築
- 事前準備（ディスク容量の確保）
`docker system prune -a`を入力して y で実施する（不要 Docker イメージを削除して空きを作る）  

**Docker**とは…  
他に実行しているプログラムから影響を受けない隔離された環境上で新たなプログラムを実行することを可能にする、コンテナ型の仮想環境を作成、配布、実行するためのソフトウェア。

- MYSQLをインストール
以下を張り付け、 MariaDBを削除してMySQL8.0をインストールする。
```vb
  curl -fsSL https://raw.githubusercontent.com/MasatoshiMizumoto/raisetech_documents/main/aws/scripts/mysql_amazon_linux_2.sh | sh
```
　Activeが **active (running)** であることを確認

- 初期パスワードの確認と動作確認  

以下を張り付け、初期パスワードを控える。  
```vb
sudo cat /var/log/mysqld.log | grep "temporary password" | awk '{print $13}'
```  
`mysql -u root -p`でEnter passwordで控えていたパスワードを入力し、セットアップが完了していることを確認。 MYSQLへログインする際もこのコマンドを使う。  


- パスワードを変更する

  MYSQLにログイン後、以下を張り付ける。
  
```vb
ALTER USER 'root'@'localhost' IDENTIFIED BY '設定するパスワード';
```

'設定するパスワード'に指定したいパスワードを入力。`FLUSH PRIVILEGES;`でパスワードを変更。 `exit`で終了。 　もう一度MYSQLへログインし、パスワードが変更されているか確認し、終了する。      
  
  
  
`cd raisetech-live8-sampre-app`でディレクトリの移動    


`cp config /database.yml.sample config/database.yml`とコマンドを入力すると、configの中の「database.yml.sample」ファイルが「database.yaml」のファイル名でコピーされる。    

**yml**（YAML　Ain’t Markup Language）とは…  
ファイルの書き方のルールの一つ。拡張子は「.yml」または「.yaml」を使用。    

database.ymlファイルのパスワードにMYSQLで設定したパスワードを入力。  

`cat\etc\my.cnf`でファイルの中のsoketを確認。  
database.ymlのsoketに張り付ける。（２カ所あり）

#### アプリケーションのインストールと動作確認  

- **Bundler**　`gem install bundler`でインストール。`bundle -v`でバージョン2.3.14であることを確認。

  - Bundlerとは…gemの依存関係やバージョンを管理するツール。  
  - gemとは…パッケージまたはパッケージ管理ツール。パッケージは便利な機能がまとまったもののこと。
    
- **Node** `nvm install 17.9.1`でnodeのインストールとバージョン指定ができる。`node -v`でバージョン確認。  

  - Nodeとは…JavaScriptランタイム環境の一つであり、デスクトップやサーバーでJavaScriptを実行するためのプログラムのこと。
  - nvm（Node Version Manager）とは… Node.jsのバージョンを管理するためのツール。
  - Node.jsとは…サーバサイドのJavaScript実行環境。 JavaScriptをブラウザ以外の環境で実行することが出来るように作られた。 
 
      
- **Yarn**　`npm install -g`でnpm経由でyarnをインストールする。`yarn -v`でバージョン確認。'npm install -g yarn@1.22.19'でバージョン指定。再び'yarn -v'で変更されていることを確認。
  - npmとは…JavaScript開発者向けのパッケージ管理ツール。Node.jsのパッケージモジュール(部品）を管理するシステムのこと。     
  - yarnとは…Node.jsのパッケージマネージャー（パッケージ管理システム）のこと。npmの問題を解決するための開発されたもの。

#### アプリケーションの起動
   `bin/setup`でRailsアプリケーションの設定を自動化。  
  `bin/cloud9_dev`でアプリケーションの起動。  
アクセス権限がなく、エラーが表示される。  
`ls -la bin`でファイルやディレクトリの情報を表示する。（表示したいファイルに移動していないと表示されない）  
パーミッションを確認するとcloud9_devは-rw-rw-r--となっており、実行権限がないことが分かる。  


**パーミッションとは**　ファイルやディレクトリの1個1個に許可属性を与え、管理する事。「所有者」「グループ」「その他ユーザー」にパラメーターの割り振りが可能。  　「読み」「書き」「実行」の3つの実行権は、英単語の頭文字をとって、以下の記号または数字で表される。

  |      |  **記号**    | **数字**   |      
  | ---- | ---- | ---- | 
  | 読むことが出来る(**R**eadable) | r | 4|
  | 書くことが出来る(**W**ritable)　| w | 2 |
  | 実行することが出来る(e**X**ecutable)　| x | 1 |
  | 何もできない　| - | 0 |

  「所有者　グループ　その他のユーザー」の順で、左から順番に記号を一つ一つ並べて表記する。
  頭文字はファイルの種別でそれ以降は３桁ずつ読んでいき、左から「読み取り権限」「書き込み権限」「実行権限」の順で表記される。  

パーミッションによく使われる種類
- 644（rw-r-r-）所有者、グループ、その他のユーザーともに読み取りは出来るが実行権限がなく、所有者のみ書き込みができる。  
- 755（rwxr-xr-x）オーナーは、読み取り、書き込み、実行すべての権限を設定できる。グループとその他の人は、書き込みだけは許されておらず、実行は可能。  
- 666（rw-rw-rw-）3つの立場は同じ権限が与えられており、読み取りと書き込みは出来るが、実行権限がない。
- 777（rwxrwxrwx）３つの立場にすべての権限がある状態。
    
`sudo chmod 775 bin/cloud9_dev`でcloud9_devのアクセス権限を変更。    
-rwxr-xr-xになり、755に変更されたことを確認。  

再度アプリケーション起動。  

![起動](/RaiseTech/lecture.png/01.png)

Brocked hostのエラーが表示される。  

configの中のenvironmentsのdevelopment.rbを開く。  

Brocked hostに記載されているconfig.hosts << "f6bead4bfa184ea2adb9887d3bfef649.vfs.cloud9.ap-southeast-2.amazonaws.com"をdevelopment.rbのendの手前に張り付ける。  
再びアプリケーションを起動する。`bin/cloud9_dev`  
![ap起動](/RaiseTech/lecture.png/02.png)  


![ap起動ブラウザ](/RaiseTech/lecture.png/03.png)    
アプリの起動に成功。  

#### APサーバーについて   
**APサーバー**とは…アプリケーションのリクエストを処理し、レスポンスをクライアントに返す役割を担う。  
railsアプリケーションとAPサーバーは連携して動作している。  

- `rails s`でRailsを起動させAPサーバーの名前とバージョンを確認。（v5.6.5）
  
 ![pumaバージョン](/RaiseTech/lecture.png/04.png)

 rails起動後、`Ctrl+Cキー`を入力してPumaを停止させる。  
 
 
  ![puma停止](/RaiseTech/lecture.png/05.png)

プレビューするとエラーが表示され、起動できなくなる。  

`rails s`で再起動ができる。 

#### DBサーバについて   

**DBサーバー**とは…データーベース管理システム（DBMS）を実行し、データーベースのアクセスを提供するサーバー。  

`mysql -u root -p`でmysqlにログインし、バージョンを確認。(v8.0.35)  
![mysql](/RaiseTech/lecture.png/06.png)  

`exit`で終了し、`sudo service mysqld stop`でmysqlを停止させる。  
![mysql停止](/RaiseTech/lecture.png/07.png)  
`rails s`を入力してもアプリケーションは起動しない。  

`sudo service mysqld start`でmysqlを起動。  
`rails s`で再度アプリケーション起動。  
![mysql起動](/RaiseTech/lecture.png/08.png)

起動後**active(running)**　になっていることを確認。  

![状態確認](/RaiseTech/lecture.png/09.png)  

### 感想

ひとつひとつのコマンドの意味を調べ、エラーの解決を探すのにかなり時間がかかった。  
小さな疑問はこまめにメモしながら解決していくしかないので、焦らずしっかり理解していきたい。

