
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
