# play_keycloak
- keycloakで遊ぶ用

## Setup
### Cli
```
git clone https://github.com/shoshohehe/play_keycloak.git
cd play_keycloak
docker-compose up
```
### Keycloak
Cliの手順を実行済み

1. Login
    - `http://localhost:8080`にアクセス
    - `admin/admin`でログイン
2. Create realm
    - realmとは
        - Keycloak上のテナント
    - 流れ(「1. Login」後)
        1. 画面左上部「master」を押下
        2. 「Create realm」を押下
        3. 任意の名前(demo-realmなど)で「Create」を押下
3. Create user
    - userの用途
        - OIDCを実施するためのユーザー
    - 流れ(「1. Login」後)
        1. 画面左上部「master」を押下
        2. 「Create realm」で作成したrealmを押下
            - テナント切り替え
        3. 左タブの「Users」を押下
        4. 「Add user」を押下
        5. 任意の名前(demo-userなど)で「Create」を押下
        6. 「Credentials」, 「Set password」 を順に押下
        7. 任意のパスワードを入力し、「Temporary」をOffにして「Save」を押下
            - 「Temporary」・・・一時パスワードかどうかを決めるパラメータ
        8. ログインできるか試す
            - `http://localhost:8080/realms/「2. Create realmで作ったrealm名」/account/`にアクセス
4. Create Client
    - 流れ(「1. Login」後)
        1. 画面左上部「master」を押下
        2. 「Create realm」で作成したrealmを押下
            - テナント切り替え
        3. 「Clients」, 「Create Clients」を押下
        4. 以下の値を入力していく
            - General Settings
                - Client type：OpenID Connect
                - Client ID：任意の名前(demo-clientなど)
                - Name：任意の名前(demo-clientなど)
            - Capability Config
                - Client authentication：on
                - Authorization：on
            - Login Settings
                - Root URL：http://127.0.0.1:3000/
                - Home URL：http://127.0.0.1:3000/
                - Valid redirect URIs：http://127.0.0.1:3000/*
        5. 「Save」を押下
        6. 「Credentials」を押下
            - Client Secretをコピーしておく

## Reference
- `https://www.keycloak.org/getting-started/getting-started-docker`
- `https://qiita.com/nagaemon/items/e1f4f7875fb1e4af5467`
