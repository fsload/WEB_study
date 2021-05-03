index.html
```{.html}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="./style.css">
    <script src="./index.js" defer></script>
</head>
<body class="body">
    <header>
        <nav class= "bar">
            <ul class="nav_img">
                <img class="menu" src="./menu.png" alt="">
                <img class="dock" src="./서랍.png" alt="">
            </ul>
        </nav>
    </header>
    <main class="main">
        <h1 class="logo"><img src="./img_logo_main_home.png" alt=""></h1>
        <div class="search-bar"></div>
            <input class="search" type="text" placeholder="검색어를 입력해주세요.">
        
        <section class="go_link"></section>
            <div class="link_wrapper">
                <a href="https://m.news.naver.com/" target="_black" class="link_item">
                    <div class="img-icon-wrapper"><img src="./news.png" alt=""></div>
                    <div class="link_text">뉴스판</div>
                <a href="https://m.search.naver.com/" target="_black" class="link_item">
                    <div class="img-icon-wrapper"><img src="./keyword.png" alt=""></div>
                    <div class="link_text">검색차트판</div>
                <a href="https://m.entertain.naver.com/" target="_black" class="link_item">
                    <div class="img-icon-wrapper"><img src="./연예판.png" alt=""></div>
                    <div class="link_text">연예판</div>
                <a href="https://m.datalab.naver.com/" target="_black" class="link_item">
                    <div class="img-icon-wrapper"><img src="./todaytem.png" alt=""></div>
                    <div class="link_text">트렌드판</div>
                <a href="https://m.mail.naver.com/" target="_black" class="link_item">
                    <div class="img-icon-wrapper"><img src="./mail.png" alt=""></div>
                    <div class="link_text">메일</div>
                <a href="https://m.cafe.naver.com/" target="_black" class="link_item">
                    <div class="img-icon-wrapper"><img src="./cafe.png" alt=""></div>
                    <div class="link_text">카페</div>
                <a href="https://m.blog.naver.com/" target="_black" class="link_item">
                    <div class="img-icon-wrapper"><img src="./blog.png" alt=""></div>
                    <div class="link_text">블로그</div>
                <a chref="https://m.naver.com/services" target="_black" class="link_item dot">
                    <div class="img-icon-wrapper">···</div>
                
                </a>
            </div>

    </main>
    
</body>
</html>
```
style.css
```{.css}
.body{
    background: white;
}

.dock{
    width: 200px;
    height: 200px;
    position: absolute;
    top: 40px;
    right: 60px;
    list-style: none;
    padding: 0;
    display: flex;
    align-items: center;
}
.menu{
    border-radius: 50%;
    width: 200px;
    height: 200px;
    position: absolute;
    top: 40px;
    left: 60px;
    list-style: none;
    padding: 0;
    display: flex;
    align-items: center;
}

.logo{
    margin-top: 300px;
    height: 200px;
    display: flex;
    justify-content: center;
    text-decoration: none;
}

.link_wrapper{
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    
}
.link_item{
    position: relative;
    margin-top: 40px;
    padding: 30px;
    
}
.img-icon-wrapper > img{
    width: 180px;
}
.img-icon-wrapper{
    width: 300px;
    height: 300px;
    border-radius:40%;
    display: flex;
    align-items: center;
    justify-content: center;
    background: #cdd2d8;
    background-size: 60px;
    
}
.dot{
    margin-bottom: 66px;
    font-size: 100px;
}
.link_text{
    display: flex;
    align-items: center;
    justify-content: center;
    text-decoration: none;
    font-size: 50px;
}
.search{
    width:1550px;
    height: 83px;
    border-radius: 3px;
    border:1px solid #0DDE8C;
    margin: auto;
    margin-top: 40px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 40px;
}

```

```{.js}
const searchInput = document.querySelector('.search')


searchInput.addEventListener('keyup', function(e){
    if(e.code === 'Enter'){
        window.open("https://search.naver.com/search.naver?where=nexearch&sm=top_hty&fbm=1&ie=utf8&query="+ e.target.value, "_blank")
    }
})


```
