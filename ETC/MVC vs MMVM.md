# MVC 패턴

- Model <-> Controller <->
### Model 
- 데이터 관리
- DB에 있는 데이터를 가져와서 다른 객체에 전달, 외부 객체로부터 입력데이터를 받아서 DB에 입력
- 웹 프론트에서 모델은 DB에 직접 접근하지 않고 API를 통해 데이터를 받고, 백앤드 API를 통해 데이터를 호출

### View
- 화면!
- model의 데이터를 화면에 그리는 역할
- 보통 html, js, css로 구성
- 사용자가 입력한 데이터를 처리해 다른 객체에 전달

### Controller
- model과 view를 연결하는 역할(model과 view는 직접적으로 연결되어 있지 않음)
- model에서 데이터를 가져와 view에 전달하고, view에서 입력된 데이터를 받아와 model에 전달