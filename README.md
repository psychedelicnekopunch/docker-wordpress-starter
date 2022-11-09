
Docker を用いて wordpress をローカル環境で開発するための環境構築サンプル。

## docker 確認

```bash
$ cd /path/to/your/project
$ docker-compose up --build
```

/app/wordpress_test をコピーして、
http://localhost:8080/ にアクセスしてみる。

```bash
$ cd /path/to/your/project/app
$ cp -rf wordpress_test wordpress

# http://localhost:8080/ にアクセスして
# success と表示されれば成功。

# 確認が終わったら wordpress を削除しておく。
$ rm -rf wordpress
```


## wordpress

http://localhost:8080/

* /app に wordpress というディレクトリを作成して wordpress 本体を入れる。
* wordpress ダウンロード先
	* https://ja.wordpress.org/download/



### データベース情報

user: root
pass: password


## phpmyadmin

http://localhost:8081/


## 本番データのコピー

もし本番データをコピーしたい場合は、
本番データベースからエクスポートした sql ファイルを wordpress.sql という名前に変更して、
/sql に格納する。


### sql ファイルを使ってデータを反映させる

```bash
$ cp /path/to/your/dl.sql /path/to/your/project/sql/wordpress.sql
$ cd /path/to/your/project
$ docker-compose up
# mysql のコンテナの NAMES をコピー
$ docker ps
# mysql のコンテナにログインする
$ docker exec -it docker-wordpress-starter-mysql-1 /bin/bash
# mysql にログイン。パスワードは password
$ mysql -u root -p
Enter password:
mysql> source /sql/wordpress.sql
# ログアウト
mysql> quit
$ exit
```


### sql/adjustment.sql

ローカル環境で開発する場合に一旦下記の SQL を叩く

```sql
UPDATE `wp_options` SET `option_value` = 'http://localhost:8080' WHERE `wp_options`.`option_id` = 1;
UPDATE `wp_options` SET `option_value` = 'http://localhost:8080' WHERE `wp_options`.`option_id` = 2;
```
