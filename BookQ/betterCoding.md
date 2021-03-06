![](https://images.velog.io/images/ouo_yoonk/post/9f8e6060-01ac-42fb-a147-2dba9a2f41bb/KakaoTalk_20201103_205456806_01.jpg)

> 프로그래밍 언어에는 다양한 개념이 존재하고, 이런 개념들은 왜 탄생한 것일까?
> 이 책의 목적은 그 '왜'를 알아내는 것이다

책 표지에 밝힌 책의 목적과 부합하는 책이다.
지금은 당연하게 쓰고 있는 개념들이 아직 세상에 나오기 전의 상황을 보여주며
어떤 문제가 생겼고, 어떤 고민을 통해 나오게 된 개념인지를 설명한다.

## 목차

- 1장. 효율적으로 언어 배우기
- 2장. 프로그래밍 언어를 조감하다
- 3장. 문법의 탄생
- 4장. 처리 흐림 제어
- 5장. 함수
- 6장. 에러 처리
- 7장. 이름과 스코프
- 8장. 형
- 9장. 컨테이너와 문자열
- 10장. 병행 처리
- 11장. 객체와 클래스
- 12장. 상속을 통한 재사용

### 스코프

- 스코프란 이름의 유효 범위다. 프로그램 전체에서 이름이 충돌하지 않도록 관리하는 것은 어려운 일이다 .그래서 이름의 유효 범위를 좁게 한정해서 관리가 편해지도록한다.

### 형

- 형은 사람이 데이터에 붙인 '추가 데이터'이다. 컴퓨터 안에 저장되어 있는 데이터는 0,1의 집합으로 표현되어 있다. 비트열로 수치 등의 여러 값들을 표현하고 비트열을 어떤 값으로 해석하는지의 방법은 사람이 마음대로 정한 약속에 불과하다. 같은 비트열이라도 **'그것을 어떤 종류의 값으로 해석할지'** 에 따라 틀린 값이 되어버린다

### 컨테이너(자료구조)

- 컨테이너에 넣은 데이터는 메모리에 저장된다. 메모리에는 정해진 크기의 상자가 정렬되어 있으며, 각 상자는 번호가 부여되어 있는 물품 보관함 같은 것이다. 컨테이너 종류에 따라서 메모리 저장 방법이 다르다. 그 차이에 따라 장단점이 생기게 된다

### 병행처리

- 복수의 처리를 시간축 상에 오버랩에서 실행하는 것을 병행처리라고 한다
- 편리한 병행 처리를 실현하기 위해 프로세스나 스레드 등의 개념이 만들어졌다.

### 상속

- 자식 클래스는 부모 클래스를 특수화한다
- 복수 클래스의 공통 부분을 부모 클래스로서 추출하면 좋다
- 상속 후 변경된 부분만을 구현하면 효율이 좋다
