# 당신의 행운의 숫자는? 나만의 n면체 주사위 위젯 만들기

이번 노드는 클래스에 대해 배운다.

> Everything in Python is an object, and almost everything has attributes and methods

파이썬에서 모든것은 객체고 속성과 메소드를 갖는다.

객체는 변수에 할당될 수 있고 함수의 인자로 넘겨질 수 있다는 것이다. 그런의미에서 파이썬에서의 모든것들은 객체다.

→ ...? 변수에 할당될 수 있고 함수의 인자로 넘겨질 수 있다는 것은 동의하겠는데, 그래서 객체다? 그게 객체의 정의인가?

이해를 위해 [객체의 정의](https://ko.wikipedia.org/wiki/객체_(컴퓨터_과학))를 좀 찾아보니 객체는 `메모리에 할당된 것`을 의미하는 듯하다. 너무 넓은 범위의 이야기였다.

아래 예시들을 보며 이해해보자.

```python
myvar = 3
myvar
```

변수는 단지 이름일 뿐이다. 데이터가 담긴 객체에 이름을 붙이는 것 뿐이다. 3이라는 객체에 이름을 myvar로 지은 것일 뿐이라는 것이다. 진짜 객체를 변수명으로 가리켜 참조할 수 있게 하는 것. 예를들면 DNS와 비슷한 개념이랄까..

```python
myword = 'cat'
myword
```

이도 너무나 마찬가지로 'cat'이라는 문자열 타입의 객체를 생성하고 myword라는 변수에 할당, 'cat'이라는 문자열 객체를 참조하는 것이다.

맨위의 정의에서 객체는 속성과 메소드를 가진다고 이야기했다. `문자열`이라는 `객체` 는 `upper` 라는 메소드를 지원한다.

```python
myword.upper()

>>> CAT
```

**id()**

`id()` 함수는 파이썬 내장함수로, 객체의 메모리 주소를 반환합니다.

```python
var = 4

id(var), id(4)
>>> (93926571806112, 93926571806112)
```

**얕은복사**

```python
mylist = [1,2,3]
var = mylist
var
>>> [1,2,3]

mylist.append(4)
mylist == var
>>> True

id(mylist) == id(var)
>>> True
```

[1,2,3] 이라는 리스트 객체를 mylist라는 변수에 할당했다. [1,2,3]를 가리키고 있는 mylist 변수를 다시 var라는 변수에 할당했으니, 결국 두 변수는 같은 곳을 바라본다. 데이터의 id값 만을 복사하였다. 이를 얕은복사라고 한다.

> 얕은복사는 객체의 주소를 복사하고, 깊은복사는 객체의 값을 복사한다.

### 객체지향 프로그래밍

------

개발자가 직접 객체를 설계하기 위해서는 `class` 를 이용해야 한다.

클래스 선언

```python
class Car:
    pass

id(Car), id(Car())
>>> (93926581692304, 139659135289184)

type(Car), type(Car())
>>> (type, __main__.Car)
```

여기서 신기한 것은 `Car` 이라는 클래스는 `type` 유형의 객체(모든것은 객체)이고, `Car()` 를 호출할 때 `Car` 타입의 객체가 된다.

클래스 사용 (객체 인스턴스화)

```python
mycar = Car()
mycar2 = Car()
id(mycar) == id(mycar2)
>>> False
```

`Car` 라는 클래스 객체를 사용하는 방법은 객체를 인스턴스화(괄호를 통해) 하는 것이다. `mycar` 라는 인스턴스와 `mycar2` 라는 인스턴스는 당연히 id값이 다르다.

PEP8

- 클래스명 → 카멜케이스 (MyCar)
- 함수명 → 스네이크 케이스 (my_car)

앞서 개발자가 직접 객체를 설계하기 위해선 `class` 를 사용해야 한다고 했고 객체는 속성과 메소드를 갖는다고 했다. 그렇다면 우리가 `class` 를 이용해서 속성과 메소드를 갖는객체를 만들어보자.

- 속성 - 상태(변수)
- 메소드 - 동작(함수)

Car라는 클래스 객체

```python
class Car:
    color = 'red'
    category = 'sports car'
		
    def drive(self):
        print("I'm driving")
				
    def accel(self, speed_up, current_speed=10):
        self.speed_up = speed_up
        self.current_speed = current_speed + speed_up
        print("speed up", self.speed_up, "driving at", self.current_speed)
```

위 객체는 `color`, `category` 라는 속성을 갖는다. 또, `drive`, `accel` 이라는 메소드를 갖는다.

이를 사용해보자.

```python
my_car = Car()

my_car.color
>>> 'red'

my_car.category
>>> 'sports car'

my_car.drive()
>>> "I'm driving"

my_car.accel(5, 10)
>>> "speed up 5, driving at 15"
```

`self` 라는 키워드만 제외하면 이해가 어렵진 않을 것이다. `self` 는 클래스 객체로 만든 인스턴스 객체를 말한다. 그러니까 위의 예제에선 `my_car` 가 해당될 수 있을 것이다.

아래의 코드는 결과적으로 같은 동작을 수행한다.

```python
my_car.drive() == Car.drive(my_car)
>>> True
```

**생성자**

우리가 만든 `Car` 객체의 인스턴스들은 선언시 다 같은 속성값을 가졌었다.  `__init__` 은 클래스를 인스턴스화 할 때, 즉 인스턴스를 만들 때 인스턴스의 `속성` 을 지정할 수 있도록 한다.

```python
class Car2:
    def __init__(self, color, category):
        self.color = color
        self.category = category

    def drive(self):
        print("I'm driving")

    def accel(self, speed_up, current_speed=10):
        self.speed_up = speed_up
        self.current_speed = current_speed + self.speed_up
        print("speed up", self.speed_up, "driving at", self.current_speed)
my_car2 = Car2('blue', 'sedan')
my_car2.color
>>> 'blue'
my_car2.category
>>> 'sedan'
```

**클래스 변수와 인스턴스 변수**

클래스 변수는 해당 클래스로 만든 인스턴스들은 다 같은 값을 갖고 인스턴스 변수는 인스턴스 생성시 할당된다. 그러니까 아래 예시에 대한 상황은 Korea에서 제조된 차량만 등록하는 클래스를 선언한 것이다.

```python
class Car:
    Manufacture = "Korea"

    def __init__(self, color, category='sedan'):
        self.color = color
        self.category = category
car1 = Car('red','sports car')
car2 = Car('blue')
car1.Manufacture, car1.color, car1.category)
>>> ('Korea', 'red', 'sports car')
car2.Manufacture, car2.color, car2.category)
>>> ('Korea', 'blue', 'sedan')
```

**상속**

이미지 정의 된 클래스 객체에 변형을 주고싶을 때 사용한다.

```python
class NewCar(Car):
		maker = 'Porsche'

car = NewCar('blue', 'sedan')
car.maker
>>> 'Porsche'
car.color
>>> 'blue'
```

**super()**

```python
class Car:
    Manufacture = "Korea"

    def __init__(self, color, category):
        self.color = color 
        self.category = category
    
    def get_color(self):
        print(self.color)
        
class NewCar(Car):
    def __init__(self):
        pass

newcar = NewCar('red', 'sports car')
print(newcar.category)
```

위의 코드를 실행시키면 어떤 결과가 나올까?? 에러가 나온다

`Car` 를 상속받는 `NewCar` 가 있다. 상속받고 `__init__()` 까지의 정의를 했다. 이때 자식 클래스의 `__init__()` 은 부모 클래스에 있는 `__init__()` 을 오버라이딩 해버린다.. 그래서 부모클래스의 `__init__()` 은 무시되는 것이다. 물론 부모 클래스에 작성되어 있는 내용을 그대로 가져와서 오버라이딩 시켜도 된다. 하지만 조금 더 간편하게 가져올 수 있다. 바로 `super()` 를 이용해서!

```python
class Car:
    Manufacture = "Korea"

    def __init__(self, color, category):
        self.color = color 
        self.category = category
    
    def get_color(self):
        print(self.color)
        
class NewCar(Car):
    def __init__(self, color, category):
        super().__init__(color, category)
        pass

newcar = NewCar('red', 'sports car')
print(newcar.category)
```

간단한 경우 단지 오버라이딩 하는것이 덜 복잡해 보일 수 있다. 하지만 조금이라도 메소드 안이 복잡해지게되면 `super()` 가 편하다는 것을 알게 될 것 같다.





#### 나만의 주사위 위젯 만들기

주사위 면을 결정하는 숫자를 인스턴스 변수로 받고 주사위 굴린다. 그리고 `getnum`을 통해 랜덤한 숫자를 출력한다.

노드에선 random.randrange 를 통해 구현했는데, 앞으로 numpy.random 을 주로 사용하게 될 것 같아 그렇게 구현해보았다.

```python
from numpy.random import choice


class FunnyDice:
    
    def __init__(self, n=6):
        self.n = int(n)

    def throw(self):
        self.num = choice(range(1, self.n + 1))

    def getnum(self):
        return self.num

    def setnum(self, num):
        if num <= self.n:
            self.num = num
        else:
            msg = "주사위에 없는 숫자입니다. 주사위는 1 ~ {0}까지 있습니다. ".format(self.n)
            raise ValueError(msg)


def get_inputs():
    n = int(input("주사위 면의 개수를 입력하세요: "))
    return n


def main():
    n = get_inputs()
    mydice = FunnyDice(n)
    mydice.throw()
    print("행운의 숫자는? {0}".format(mydice.getnum()))


if __name__ == '__main__':
    main()

```

