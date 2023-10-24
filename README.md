# express-server

## 初期化
- DB初期化
```
cd db
npm install
make initv
make initn
make up-db
npm run sequelize db:create
npm run sequelize db:migrate
```

- backendサーバー起動
```
cd server
npm install
```

- frontend起動
```
cd front-app
npm install
```


## 起動方法

- DB起動
```
cd db
make up-db
```

- backendサーバー起動
```
cd server
npm run dev
```

- frontend起動
```
cd front-app
npm run dev
```
