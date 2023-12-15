---
layout: post
title: ""
date: 2015-02-08T20:39:51-09:00
modified: 2015-02-08T22:21:31-09:00
categories: articles
excerpt: "맵(Map)과 해시 테이블(hash table)"
tags: [oowgnod]
image:
  feature: test.jpg
  credit: Me
  creditlink: me.org
share: true
comments: true
---

자바스트립트 알고리즘 문제풀이를 하다가 쉬워보이는 문제가 잘 풀리지 않아 정리한 내용을 메모장 처럼 끄적여보았습니다

---

문제

> 학급 회장  
>   
> 학급 회장을 뽑는데 후보로 기호 A, B, C, D, E 후보가 등록을 했습니다.  
> 투표용지에는 반 학생들이 자기가 선택한 후보의 기호(알파벳)가 쓰여져 있으며 선생님은 그 기호를 발표하고 있습니다. 선생님의 발표가 끝난 후 어떤 기호의 후보가 학급 회장이 되었는지 출력하는 프로그램을 작 성하세요.  
> 반드시 한 명의 학급회장이 선출되도록 투표결과가 나왔다고 가정합니다.  
>   
> ▣ 입력설명 첫 줄에는 반 학생수 N(5<=N<=50)이 주어집니다. 두 번째 줄에 N개의 투표용지에 쓰여져 있던 각 후보의 기호가 선생님이 발표한 순서대로 문자열로 입력됩니다.  
> ▣ 출력설명 학급 회장으로 선택된 기호를 출력합니다.  
> ▣ 입력예제 1 15 BACBACCACCBDEDE  
> ▣ 출력예제 1 C

해당 문제는 자바스크립트의 new Map 과 그에 맞는 메서드들을 활용하면 쉽게 해결할수있는 문제였습니다.

하지만 map과 hash table의 기본적인 지식 부족으로 풀지 못 하여 아래의 내용을 정리 해보았습니다.

---

## Map

\-key-value pair들을 저장하는 **ADT**

_ADT란?_

_추상 자료형(Abstract Data Type,ADT)_

_구현하고자 하는 구조에 대해 구현 방법은 명시하지 않고 자료구조의 특성들과 어떤 Operations들이 있는지를 설명하는 자료구조의 한가지 형태 일종의 규칙들의 나열이라고 볼수있다._

\- 같은 key를 가지는 pair는 최대 한 개만 존재

\- JS에서 key로 사용할 수 있는 데이터형은 string,symbol(ES6),object,function number는 사용할 수 없음

\- associative array, dictionary라고 불리기도 함

Map의 예시

| 노래 제목 | 가수 |
| --- | --- |
| Cry baby | Official髭男dism |
| Lemon | 요네즈 켄시 |
| IDOL | YOASOBI |

노래 제목이 key 가수가 value가 됨

| Official髭男dism | 52 |
| --- | --- |
| 요네즈 켄시 | 44 |
| YOASOBI | 31 |

또는 인기투표를 한다고 가정 했을때 처럼 투표의 경우에도 사용할수있다.

### Map의 구현체

#### Hash table(hash map)

\- 배열과 해시 함수(hash function)를 사용하여 map을 구현한 자료 구조

\- 상수 시간으로 데이터에 접근하기 떄문에 빠르다

#### Hash function

\- 임의의 크기를 가지는 type의 데이터를 고정된 크기를 가지는 type의 데이터로 변환하는 함수

\- 임의의 데이터를 정수로 변환하는 함수

Hash collision

\- key는 다른데 hash가 같을때

\- key도 hash도 다른데 hash % map\_capa결과가 같을 때

해결방법

\- open addressing

\- separate chaining

## 자바스크립트 맵 객체(Map Object)

맵은 객체와 달리 key를 문자형으로 변환하지 않습니다. key에는 자료형이 없습니다.

new Map() – 맵을 만듭니다.

```
let map1 = new Map([ // 2차원 key, value 형태의 배열
    ['a',1],
    ['a1',2],
    ['b',3]
])
// map 자료형 : {"a" => 1, "a1" => 2, "b" => 3}
```

map.set(key, value) – key를 이용해 value를 저장합니다.

map.get(key) – key에 해당하는 값을 반환합니다. key가 존재하지 않으면 undefined를 반환합니다.

map.has(key) – key가 존재하면 true, 존재하지 않으면 false를 반환합니다.

map.delete(key) – key에 해당하는 값을 삭제합니다.

map.clear() – 맵 안의 모든 요소를 제거합니다.

map.size – 요소의 개수를 반환합니다.

```
const contacts = new Map();
contacts.set("Jessie", { phone: "213-555-1234", address: "123 N 1st Ave" });
contacts.has("Jessie"); // true
contacts.get("Hilary"); // undefined
contacts.set("Hilary", { phone: "617-555-4321", address: "321 S 2nd St" });
contacts.get("Jessie"); // {phone: "213-555-1234", address: "123 N 1st Ave"}
contacts.delete("Raymond"); // false
contacts.delete("Jessie"); // true
console.log(contacts.size); // 1
```

> ​map\[key\]는 Map을 쓰는 바른 방법이 아닙니다.  
> map\[key\] = 2로 값을 설정하는 것 같이 map\[key\]를 사용할 수 있긴 합니다. 하지만 이 방법은 map을 일반 객체처럼 취급하게 됩니다. 따라서 여러 제약이 생깁니다.  
> map을 사용할 땐 map전용 메서드 set, get 등을 사용해야만 합니다.

Map()을 사용하여 위 내용을 코드로 구현해보면

```
function solution(s){  
                let answer;
                let sH = new Map();
                for(let x of s){
                    if(sH.has(x)) sH.set(x, sH.get(x)+1);
                    else sH.set(x, 1);
                }
                let max=Number.MIN_SAFE_INTEGER;
                for(let [key, val] of sH){
                    if(val>max){
                        max=val;
                        answer=key;
                    }
                }
                return answer;
            }

            let str="BACBACCACCBDEDE";
            console.log(solution(str));
```
