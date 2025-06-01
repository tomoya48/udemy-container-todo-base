

## ローカル開発準備
init.sqlのタスクの更新日時を変更。稼働確認できるように、翌日などにする

PostgresのDockerを起動
```bash
docker-compose -f .\docker-compose-postgres.yml up -d
```

Postgresコンテナのログを確認
```bash
docker logs postgres_db
```

Postgresのコンテナに入る
```bash
docker exec -it postgres_db psql -U udemy_learn_user -d udemy_learn_db
```

テーブル一覧を確認
```sql
\dt
```

テーブルの中身を確認
```sql
\d todos
```

```sql
SELECT * FROM todos;
```

```sql
\q
```

#### そのほか
DockerのVolumeを削除
```bash
docker volume rm udemy-container-todo-app_postgres_data
```

## ローカル開発
### ToDoアプリ
.envファイルを作成し、以下の内容を記述します。
```env
POSTGRES_USER=udemy_learn_user
POSTGRES_PASSWORD=udemy_learn_password
POSTGRES_DB=udemy_learn_db
POSTGRES_HOST=localhost
POSTGRES_PORT=5432
POSTGRES_SSLMODE=disable
```

モジュールをインストールします。
```bash
npm install
npm run dev
```

### 通知サービス
.envファイルを作成し、以下の内容を記述します。
```env
POSTGRES_USER="udemy_learn_user"
POSTGRES_PASSWORD="udemy_learn_password"
POSTGRES_DB="udemy_learn_db"
POSTGRES_HOST="localhost"
POSTGRES_PORT="5432"
POSTGRES_SSLMODE="disable"
SENDER_EMAIL="メールアドレス"
EMAIL_PASSWORD="Gmailのアプリパスワード"
RECIPIENT_EMAIL="メールアドレス"
SLEEP_SECONDS="3600"
```

venvを作成し、F5実行


## Dockerビルドと起動

### ToDoアプリの環境変数ファイル
.env.local.containerファイルを作成し、以下の内容を記述します。
```env
POSTGRES_USER=udemy_learn_user
POSTGRES_PASSWORD=udemy_learn_password
POSTGRES_DB=udemy_learn_db
POSTGRES_HOST=postgres_db
POSTGRES_PORT=5432
```

### notifyサービスの環境変数ファイル
.env.local.containerファイルを作成し、以下の内容を記述します。
```env
POSTGRES_USER="udemy_learn_user"
POSTGRES_PASSWORD="udemy_learn_password"
POSTGRES_DB="udemy_learn_db"
POSTGRES_HOST="postgres_db"
POSTGRES_PORT="5432"
POSTGRES_SSLMODE="disable"
SENDER_EMAIL="メールアドレス"
EMAIL_PASSWORD="Gmailのアプリパスワード"
RECIPIENT_EMAIL="メールアドレス"
SLEEP_SECONDS="3600"
```

docker-compose.local.ymlを使用して、Dockerイメージをビルドして起動します。
```bash
docker-compose -f docker-compose.local.yml up -d
```

