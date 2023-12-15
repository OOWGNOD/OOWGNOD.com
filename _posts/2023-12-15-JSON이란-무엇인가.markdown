> JSON(JavaScript Object Notation)은 Javascript 객체 문법으로 구조화된 데이터교환 형식, python, javascript, java 등 여러 언어에서 데이터 교환형식으로 쓰이며 객체문법 말고도 단순 배열, 문자열도 표현이 가능하다

## 1\. Javascript 객체 문법 

Javascript 객체는 키(key)에 대응하는 값(value)으로 구성되어 있다.

```
{

key: value

}
```

#### 1\. 만약 이미 존재하는 키를 중복선언하면 어떻게 될까?

나중에 선언한 해당 키에 대응한 값이 덮어쓰이게 된다.

```
{
"name" : "ongdoo",
"name" : "ongdoodev",
"age" : 26
}
```

이렇게 키가 name 으로 중복선언됐다라고 가정 했을 경우

나중에 선언된 키에 대응한 값이 덮었으이게 된다.

```
{
"name":"ongdoodev",
"age":26
}
```

결국 JSON 형식에서는 키(key) 값이 중복되지 않도록 신경 써주는 것이 좋다.

## 2\. 데이터 + 교환형식

데이터는 추상적인 아이디어에서부터 시작해 구체적인 측정에 이르기까지 다양한 의미로 쓰인다. 실험, 조사, 관찰 등으로부터 얻은 사실이나 자료 등을 의미한다.

JSON 은 데이터를 주고받을 때 사용하는 양식과도 같다.

이때 JSON은 여러 언어, 플랫폼에 대해서 독립적이다.

예를 들면 Javascript, python과 같은 언어의 버전 업데이트가 있다고 해서 JSON을 변경할 필요가 없다는 뜻이다.

단지 그 언어에 맞춰 JSON을 변형해서 사용하기만 하면 된다.

ex) Javascript - JSON.parse , python - JSON.loads...

## 3\. JSON 은 단순 배열, 문자열로도 표현이 가능하다.

```
[1,2,3,4,5,6]
```

```
"이것도 JSON 이긴함 ㄹㅇㅋㅋ"
```

보통 이렇게 사용하지는 않는다.

## 4\. JSON으로 표현해 보자

```
const JPOP = {
	"JPOP띵곡" : [{
    	"name" : "official hige dandism",
        "song" : "pretender"
    },
    { 
    	"name" : "DAOKO",
        "song" : "Uchiagehanabi"
    }
    ]
}

console.log(JPOP.JPOP띵곡, 
	"{
    	"name" : "official hige dandism",
        "song" : "pretender"
    },
    { 
    	"name" : "DAOKO",
        "song" : "Uchiagehanabi"
    }"
);
console.log(JPOP.JPOP띵곡[0],
	"{
    	"name" : "official hige dandism",
        "song" : "pretender"
    }"   
);
console.log(JPOP.JPOP띵곡[0].name, 
	"official hige dandism"
);
```

이때 값(value)의 값들이 모두 String type 인걸 볼 수 있는데

사실 값(value)에는 String이 아니라 다른 type의 값이 들어와도 상관없다.

하지만 우리가 데이터를 구축할 때는 스키마(schema)를 잘 구축해주어야 한다.

예를 들면 데이터를 주고받을 때

어떨 때는 name이 String이고 

어떨 때는 name이 Number이면

이 데이터가 들어올 때마다 type checking 등의 추가 작업이 필요해지기 때문에

이 데이터의 type이 어떤 것이 들어올 것이다라는 약속이 필요하다.

## 5\. JSON의 타입

JSON의 타입은 Javascript object와 유사하지만

undefined, method 등을 포함하지 않습니다.

\-수(Number)

\-문자열(String)

\-참/거짓(Boolean)

\-배열(Array)

\-객체(Object)

\-null

```
const a = {
	"a" : () => {
	console.log(1)
         },
         {
         "b" : undefined
         }
}​
```

이런 형식은 JSON의 type은 아니다.

---

#### JSON의 직렬화,역직렬화

> 직렬화,역직렬화란?  
> 직렬화란 외부의 시스템에서도 사용할 수 있도록 바이트(byte) 형태로 데이터를 변환하는 기술이며  
> 역직렬화는 반대를 의미한다.  
>   
> ex) JSON.parse() <=> JSON.stringify()

#### 직렬화

jsObject 에서 다시 바이트(byte)형태로 바꿔준다. ( JSON.stringify() )

dict 에서 다시 바이트(byte)형태로 바꿔준다. ( json.dumps() )

#### 역직렬화

Javascript에서는 jsObject 로 만들어줘야한다. ( JSON.parse() )

python 에서는 dict로 만들어줘야한다. ( json.loads() )
