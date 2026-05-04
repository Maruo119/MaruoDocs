
# Github CLI

## 別のIAMユーザーに切り替えたい場合はどうしたらよい？

#### 現在の設定を上書きする（一番簡単）
単に今のユーザーを新しいユーザーに差し替えたいだけであれば、もう一度 aws configure を入力し、新しい情報を入力するだけで上書きされます。

端末で aws configure を実行。

AWS Access Key ID が表示されたら、新しいキーを入力してエンター。

AWS Secret Access Key も新しいものを入力。

Region や Output format はそのままで良ければ、何も入力せずエンター。

これで、デフォルトのユーザーが切り替わります。

## AWS Secret Managerについて、コマンドラインからシークレット情報を追加する場合はどうしたらよい？

### 登録方法
#### ①単純なテキスト（文字列）を保存する場合
パスワードなどの単一の文字列を保存する場合は --secret-string を使います。

```bash
aws secretsmanager create-secret `
    --name "MyTestSecret" `
    --description "テスト用のパスワードです" `
    --secret-string "my-super-secure-password"
```

#### ②キーと値のペア（JSON）を保存する場合
「ユーザー名」と「パスワード」のように、複数の情報をセットで保存したい場合に最もよく使われる方法です。

```bash
aws secretsmanager create-secret `
    --name "MyApp/Prod/Database" `
    --secret-string '{"username":"admin","password":"ExamplePassword123"}'
```

### 確認方法
登録後、以下のコマンドで内容を表示して確認できます。

```bash
aws secretsmanager get-secret-value --secret-id "MyTestSecret"
```
