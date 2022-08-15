## test
mongoDB接続コード
```server.js
    //mongodb接続
mongoose.connect(
    process.env.MONGOURL
).then(() => {
    console.log("db connect");
}).catch((err) => {
    console.log(err);
});
```