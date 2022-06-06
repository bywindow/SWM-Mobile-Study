---
title: [mobile-study] week1. 함수형 프로그래밍
date: 2022-06-07
---
## 🐛 순수함수
수학에서의 함수란 $y = f(x)$ 꼴로 동일한 input x에 대해서 항상 동일한 output y를 가지는 것을 말한다. 이 개념을 프로그래밍으로 옮긴 것이 **순수함수**이다.
![image.png](https://i0.wp.com/www.techdiscuss.net/wp-content/uploads/2020/08/Pure-functions.png?fit=666%2C507&ssl=1)
함수의 실행이 전체 프로그램의 실행에 영향을 미치면 안된다. 즉, 함수 내부에서 외부의 값을 변경하는 것과 같은 Side Effect(부작용)가 나면 안된다.

## 🧊 함수형 프로그래밍의 정의
함수형 프로그래밍(Functional Programming)은 코드를 작성하는 스타일 중 하나이다.
즉, 함수형 프로그래밍으로 설계된 언어가 따로 존재하지만(Clojure, Scala), 우리가 사용하는 모든 언어에 적용할 수 있으며 프로그래밍에 발생할 수 있는 여러 문제들을 해결할 수 있다.
다시 정리하면, **함수형 프로그래밍**은 공유 상태, 변경 가능한 데이터, 부작용을 피하는 기본 원칙에 따라 소프트웨어를 구성하는 프로그래밍 패러다임이다.
>객체지향은 동작하는 부분을 캡슐화해서 이해할 수 있게 하고, 함수형 프로그래밍은 동작하는 부분을 최소화해서 코드 이해를 돕는다. (마이클 페더스‘레거시 코드 활용 전략’)

![programming history](https://dinfree.com/assets/blog-img/java-fp-1.png)

## 명령형 vs 선언형