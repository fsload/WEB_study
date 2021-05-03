```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-giJF6kkoqNQ00vy+HMDP7azOuL0xtbfIcaT9wjKHr8RbDVddVHyTfAAsrekwKmP1" crossorigin="anonymous">
    <title>Document</title>
    <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.5.4/dist/umd/popper.min.js" integrity="sha384-q2kxQ16AaE6UbzuKqyBE9/u/KzioAlnx2maXQHiDX9d4/zp8Ok3f+M7DPm+Ib6IU" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta1/dist/js/bootstrap.min.js" integrity="sha384-pQQkAEnwaBkjpqZ8RU1fF1AKtTcHJwFl3pblpTlHXybJjHpMYo79HY3hIi4NKxyj" crossorigin="anonymous"></script>
</head>
<body>
    <div class="container">
        <select name="" id="">
            <option value="idx">인덱스 별</option>
            <option value="name">이름 별</option>
            <option value="max">최대값 별</option>
            <option value="min">최소값 별</option>
            <option value="avg">평균값 별</option>
            <option value="day">1일 변동률 별</option>
        </select>
    </div>
    <script>
        (async function (){
            const bitInformation = await axios.get(
                'https://api.bithumb.com/public/ticker/ALL'
            )
            const {data} = bitInformation
            let entry = Object.entries(data.data)

            const trTag = (data, index) => `
                <tr>
                        <th scope="row">${index}</th>
                        <td>${data[0]}</td>
                        <td>${Number(data[1]['max_price']).toLocaleString()}</td>
                        <td>${Number(data[1]['min_price']).toLocaleString()}</td>
                        <td>${((Number(data[1]['max_price']) + Number(data[1]['min_price']))/2).toLocaleString()}</td>
                        <td>${Number(data[1]["fluctate_rate_24H"]).toLocaleString()}</td>
                </tr>
            `
            function createTable(data){
                const trs = data.reduce((acc, cur, index) => {
                    acc += trTag(cur,index)
                    return acc
                }, '')

                return `
                    <table class="table">
                        <thead>
                            <tr>
                                <th scope="col">#</th>
                                <th scope="col">화폐이름</th>
                                <th scope="col">최대값</th>
                                <th scope="col">최소값</th>
                                <th scope="col">평균값</th>
                                <th scope="col">1일 변동율</th>
                            </tr>
                        </thead>
                        <tbody>
                        ${trs}
                        </tbody>
                    </table>

                    `

            }

            const switchTable = (opt) => {
                if(opt === 'idx'){
                    entry = Object.entries(data.data)
                }
                if(opt === 'name'){
                    entry.sort((a,b)=>{
                        if(a[0]>b[0]) return 1
                        else if(a[0]<b[0]) return -1
                    })
                }
                if(opt === 'max'){
                    entry.sort((a,b)=>{
                        if (Number(a[1]["max_price"]) > Number(b[1]["max_price"])) return -1
                        else return 1;
                    })
                }
                if(opt === 'min'){
                    entry.sort((a,b)=>{
                        if (Number(a[1]["min_price"]) > Number(b[1]["min_price"])) return -1
                        else return 1;
                    })
                }
                if(opt === 'avg'){
                    entry.sort((a,b)=>{
                        if (((Number(a[1]['max_price']) + Number(a[1]['min_price']))/2) > ((Number(b[1]['max_price']) + Number(b[1]['min_price']))/2)) return -1
                        else return 1
                    })
                }
                if(opt === 'day'){
                    entry.sort((a,b)=>{
                        if(Number(a[1]["fluctate_rate_24H"]) > Number(b[1]["fluctate_rate_24H"])) return 1
                        else return -1
                    })
                }
            }
            
            document.querySelector(".container").insertAdjacentHTML('beforeend', createTable(entry))

            const select = document.querySelector('select')
            const tab = document.querySelector(".container");

            select.addEventListener('change', (event) => {
                let opt = event.target.value
                switchTable(opt)
                tab.removeChild(document.querySelector('table'));
                document.querySelector(".container").insertAdjacentHTML('beforeend', createTable(entry))
            })
        })()
    </script>
</body>
</html>
 ```
![image](https://user-images.githubusercontent.com/60029949/116840054-7f96ac80-ac0f-11eb-8c61-5d148cba90ff.png)
![image](https://user-images.githubusercontent.com/60029949/116840073-8e7d5f00-ac0f-11eb-82dc-f2a433b797d7.png)

![image](https://user-images.githubusercontent.com/60029949/116840092-9f2dd500-ac0f-11eb-9e04-2382d41ceb03.png)


