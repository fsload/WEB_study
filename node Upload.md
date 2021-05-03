index.js
``` javascript
const express = require('express');
const multer = require('multer');
const fs = require('fs');
const path = require('path');
const e = require('express');
const { restart } = require('nodemon');
const app = express();

app.set('view engine', 'ejs')
app.use(express.urlencoded({extended:false}));
app.use(express.json());

app.get('/', (req, res) =>{
    console.log(__dirname)
    res.render('index')
})

const upload = multer({
    storage: multer.diskStorage({
        destination: (req, file, done) => {
            done(null, 'uploads/')
        },
        filename: (req, file, done) => {
            const ext = path.extname(file.originalname)
            done(null, path.basename(file.originalname, ext)+ Date.now() + ext)
        }
    }),
    limits: {fileSise : 5 + 1024 + 1024}
})

app.post('/upload', upload.single("userfile"), (req, res) =>{
    console.log(req.file)
})

app.get('/download', async(req, res) =>{
    try{
        res.set('Content-Disposition', `attachment; filename=downloadFromServer.png`)
        res.set('Content-Type', 'application/octet-stream');
        const file = fs.createReadStream(`${__dirname}/uploads/123.png`);
        return file.pipe(res);
    } catch (error) {
        console.log(error)
    }
})


app.listen(8000, () => console.log('서버 8000'))
```
index.ejs
``` ejs
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <!-----일반파일 업로드---->
    <form method="post" enctype="multipart/form-data" action="./upload">
        <input type="file", name="userfile">
        <input type="submit" value="전송하기">
    </form>

    <br/>
    <br/>
    <hr/>


    <a href="/download">download</a>

</body>
</html>
```

![image](https://user-images.githubusercontent.com/60029949/116840228-08154d00-ac10-11eb-8d32-410b2f5f2eba.png)
