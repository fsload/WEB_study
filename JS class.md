```javascript

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script>
        class Person{
            constructor(name,hp){
                this.name = name
                this.hp = Number(hp)
            }
            hello(){
                console.log(`name = ${this.name}`)
            }
        }
        class Avengers extends Person{
            constructor(name, hp, power, skill){
                super(name, hp)
                this.power = power
                this.skill = skill
            }
            information(){
                console.log(`name = ${this.name} HP = ${this.hp} power = ${this.power} skill = ${this.skill}`)
            }
            fly(){
                console.log(`비행중`)
            }

        }
        
        let p = new Person('로버트 다우니 주니어', 100)
        p.hello()

        let q = new Avengers('아이언맨', 100, 'overwhelming', 'fly')
        q.information()
        q.fly()
    </script>
</body>
</html>

```
![image](https://user-images.githubusercontent.com/60029949/116839938-0e56f980-ac0f-11eb-93b3-a754574db77c.png)
