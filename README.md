# express_output

エクスプレスのサーバーとなるファイルであり、エントリーポイントの代表的な設定。
ミドルウェアによってルートを分けている。
mongooseでmongoDBに接続する方法も記載。

```js
const express = require('express');

const app = express();
const userRoute = require("./routes/users");
const authRoute = require("./routes/auth");
const postRoute = require("./routes/posts");
const uploadRoute = require("./routes/upload");
const port = 3001;
const mongoose = require("mongoose");
const path = require("path");
require("dotenv").config();

//mongodb接続
mongoose.connect(
    process.env.MONGOURL
).then(() => {
    console.log("db connect");
}).catch((err) => {
    console.log(err);
});

//ミドルウェア
app.use("/images", express.static(path.join(__dirname, "public/images")));
app.use(express.json());
app.use("/api/users", userRoute);
app.use("/api/auth", authRoute);
app.use("/api/posts", postRoute);
app.use("/api/upload", uploadRoute);

app.get("/", (req, res) => {
    res.send("aiueo")
})

// ポート番号を付与したアクセスURLを実行
app.listen(port, () => {
    console.log(`App listening at http://localhost:${port}`);
})

```
