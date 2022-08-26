## setup
### 環境構築方法
1. docker-compose.yml内のplatformを変更する
intel Macの場合は`platform: linux/amd64`のみにする（platform: linux/x86_64を削除する）
M1 Macの場合は`platform: linux/x86_64`のみにする（platform: linux/amd64を削除する）

2. dockerに関するコマンドを実行する
```
docker-compose up
```

下記のようなログが出力される(databaseが存在しないというエラー)
※ブラウザで`http://localhost:3000`にアクセスして確認できる

```
be-app | => Booting Puma
be-app | => Rails 6.0.5.1 application starting in development 
be-app | => Run `rails server --help` for more startup options
be-app | Puma starting in single mode...
be-app | * Version 4.3.12 (ruby 3.0.2-p107), codename: Mysterious Traveller
be-app | * Min threads: 5, max threads: 5
be-app | * Environment: development
be-app | * Listening on tcp://0.0.0.0:3000
be-app | Use Ctrl-C to stop
be-app | Started GET "/" for 172.22.0.1 at 2022-08-26 14:28:25 +0000
be-app |   
be-app | ActiveRecord::NoDatabaseError (Unknown database 'be_development'):
```

3. databaseを作成する
```
docker exec -it be-app bundle exec rails db:create
```

```
Created database 'be_development'
Created database 'be_test'
```

4. 
ブラウザで`http://localhost:3000`にアクセスして確認できる

### bundleのバージョンについて
herokuの対応バージョンが2.1.4のためこのバージョンに固定しています
ローカルでのインストール方法
　※Gemfile.lockを削除した上で実行すること
```
gem install bundler -v 2.1.4
bundle _2.1.4_ install
```
