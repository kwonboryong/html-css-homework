# avatars
- 아바타 이미지를 4개씩 2줄로 정렬한다. <br/>
- 아바타 이미지는 콘텐츠 이미지로 마크업 한다. <br/>
- 아바타의 상태 정보를 알 수 있는 정보를 제공한다. <br/>
- 이미지와 상태 정보는 정해진 크기로 설정한다. <br/>
- float로 구현한 뒤 flex가 지원되는 환경에서 적용될 레이아웃도 구현한다.

<br/> 
<br/>

## HTML 구조
- 아바타 이미지를 넣을 ```<img>``` 태그와 상태 정보를 나타낼 ```<div>``` 태그를 face라는 ```<div>``` 태그로 묶었다.  <br/>

- 이미지를 4개씩 묶어 box1과 box2라는 ```<div>``` 태그로 감쌌고, 이미지들을 화면의 가운데 정렬을 위해 container라는 ```<div>``` 태그로 감쌌다.  <br/>

- 상태 정보를 나타내는 ```<div>``` 태그의 class를 online(접속)과 offline(미접속)으로 나누어 아바타의 접속 여부를 확인할 수 있도록 하였다.

- 웹 접근성 향상을 위해 이미지와 상태 정보 태그에 aria-label 속성을 부여하였다.  <br/>

<br/>
<br/>

## CSS 구현
### float로 구현
![float 과제](https://github.com/kwonboryong/homework/blob/main/images/float%20%EA%B3%BC%EC%A0%9C.png?raw=true)
- 상태 정보를 나타내는 online과 offline 클래스는 border-radius를 사용하여 원 모양으로 만들었고, position: absolute 속성과 top, left 속성을 이용하여 이미지 위에 배치하였다.

- 이미지와 상태 정보를 묶는 박스인 face에는 float를 사용하여 이미지들이 가로 정렬되도록 하였고, margin-left 속성을 이용하여 이미지 간의 간격이 20px이 되도록 구현하였다. 
그리고 자식 요소인 상태 정보 클래스 online과 offline에 position: absolute 속성을 부여하기 위해 부모 요소인 face에 position: relative 속성을 부여하였다.

- 두 번째 이미지 박스인 box2 클래스에 padding-top을 이용하여 이미지 박스 간의 간격을 설정하기 위해 clear: both를 적용하였다.

- 전체 태그를 감싼 container 클래스에는 position: absolute 속성과 top, left 속성을 이용하여 화면 가운데로 이동하도록 하였다.

 <br/>

- #### 문제 & 해결
  - **1. 가운데 정렬**  <br/>
container에 margin을 줘서 가운데 정렬하려고 했는데 이 방법은 비효율적인 것 같아서 다른 방법을 생각해보았다.  <br/>
container에 position: absolute를 적용하여 부모 요소인 html 태그를 기준으로 top과 left를 적용하여 가운데 정렬시켰다.

  - **2. 이미지 박스 간 간격**  <br/>
box2에 margin-top을 주어 box1과 box2 간의 간격을 설정하려고 했다.  <br/>
그러나 margin도 padding도 적용되지 않았고 float 영향 때문인가 싶어 .box2에 clear: both를 적용한 뒤 padding-top을 적용하니 원하는 간격으로 조정되었다.

<br/> 
<br/> 
<br/>

### flex로 구현
![flex 과제](https://github.com/kwonboryong/homework/blob/main/images/flex%20%EA%B3%BC%EC%A0%9C.png?raw=true)
- flex 기능이 적용되는 환경에서의 레이아웃을 위해 기존의 float로 구현한 코드에서 @supports를 사용하여 flex 코드를 추가하고 float가 적용된 코드들을 변경하였다.

- 이미지와 상태 정보를 묶는 박스인 face에는 이미지 간격을 위한 margin-left 속성과 자식 요소인 상태 정보 클래스 online과 offline에 position: absolute 속성을 부여하기 위한 position: relative 속성만 적용하였다.

- 첫 번째 이미지 박스인 box1에 display: flex를 적용하여 박스 안의 이미지들이 가로 정렬되도록 했고, order: 2를 부여하여 두 번째 이미지 박스인 box2의 아래에 배치되도록 하였다. 그리고 padding-top을 주어 이미지 박스 간의 간격을 설정하였다.

- 두 번째 이미지 박스인 box2에도 display: flex를 적용하여 박스 안의 이미지들이 가로 정렬되도록 하였다.

- 전체 태그를 감싼 container 클래스에는 자식 요소인 box1과 box2의 순서 변경을 위해 display: flex를 부여하였다.  <br/> 그리고 flex-flow: column nowrap을 설정하여 가로로 정렬된 이미지 박스들을 2줄로 배치하였다. position: absolute 속성과 top, left 속성을 이용하여 화면 가운데로 이동하도록 하였다.

<br/>

- #### 문제 & 해결
  - **1. 순서 변경** <br/>
box1과 box2에 order을 부여해서 이미지 박스 채로 순서를 바꾸고 싶었는데 그러려면 container에 display: flex를 부여해야 했고, container에 flex가 부여되면 2줄이 안된다...고 생각했었다!
이미지 하나하나에 다 order을 부여하기엔 너무 비효율적이고 주먹구구식이라 이미지 박스 채로 order을 줄 수 있는 방법을 생각해보다가 flex-flow가 생각났다. flex-flow를 column, nowrap으로 주면 박스를 2줄로 배치하면서 자식 요소인 box1, box2에 order을 부여할 수 있도록 부모 요소인 container에 display: flex를 줄 수 있다!

  - **2. aria-label의 순서** <br/>
  ![float 과제의 aria-label 순서](https://github.com/kwonboryong/homework/blob/main/images/flex%20%EA%B3%BC%EC%A0%9C%20%EC%A0%91%EA%B7%BC%EC%84%B1%20%EB%AC%B8%EC%A0%9C.png?raw=true)
이미지와 상태 정보의 html 태그에는 float 과제의 이미지 순서대로 인덱싱을 붙인 aria-label 속성을 부여했다.<br/>
그러나 flex 과제는 float 과제에서 이미지 순서를 바꾸는 과제였다.
flex 과제에서 원래 float 과제에서 짜놓은 html 구조를 CSS 기능인 order 사용해서 순서만 바꾸었더니 html 구조 순서대로 인식되는 aria-label이 flex 과제의 이미지 순서가 아닌 기존의 float 과제의 이미지 순서대로 정렬되었다. 
한 마디로 flex 과제에서 실제 화면에 보이는 이미지의 순서와 aria-lable의 순서가 다른 문제가 발생한 것이다. <br/> <br/>
스크린 리더는 html 구조 순서에 따르니 html 태그 순서를 변경하는 방법 말고는 다른 해결 방법은 없는 것 같았다. <br/>
혹시나 aria-label의 순서를 변경할 수 있는 방법이 있나 찾아보았지만 찾을 수 없었다. 그렇다고 aria-label 속성에 인덱싱을 제거하자니 너무 단조로워 프로필 이미지들이 구분되지 않을 것 같았다.<br/>
결국 aria-label의 순서 문제는 해결하지 못했다.

 <br/> <br/><br/>

## 배운점
- **float가 적용되는 방식에 대해 자세히 알게 되었다.** <br/>
물론 float를 완전히 익힌 것까지는 아니지만 어떻게든 원하는 모양으로 배치할 수 있게 되었다.  <br/>
기존에 공부했던 flex와 grid가 쉽고 편해서 굳이 float를 알 필요가 없을거라고 생각했는데 이번 과제로 직접 float를 사용해보니 float는 flex, gird와는 다르게 더 섬세하게 배치할 수 있는 속성이라는 것을 깨닫게 되었다.
 <br/>

- **더불어 position 속성에 대해서도 익히게 되었다.** <br/>
position 속성은 이론으로 공부하기만 했지 직접 사용하는 것은 처음이었다.
이론만 알고 있으니 어디에 어느 상황에 사용해야 하는지 감도 잡히지 않았는데 이번 과제로 position 사용법과 적용 상황에 대해 알게 되어 기뻤다.
 <br/>

- **웹 접근성 측면에서 고려해보게 되었다.** <br/>
개발자가 되기 위해 제일 처음 들었던 강의에서 진정한 개발자는 웹 접근성을 반드시 고려해야 한다는 말을 들었었다.  <br/>
당시에는 웹 접근성에 대한 이해도가 낮고 빨리 기술부터 익히고 싶다는 욕심에 강사님이 왜 그렇게 접근성을 강조하셨는지 이해하지 못했다. 
그 뒤로도 접근성이 고려된 코드다운 코드가 아닌 div 뭉텅이를 만들어냈었고 동작하니 되었다는 마음 뒷편에는 접근성 따위 없는 코드에 양심이 찔렸었다.  <br/>
이번 기회에 접근성에 대해 제대로 배우고 직접 적용해볼 수 있어서 기쁘고 뿌듯했다. <br/> <br/>
아직 어색하고 낯설어서 이렇게 구성하는게 맞는지, alt와 aria-label을 어떻게 작성해야 할지 몰라서 엉성한 코드 투성이지만 이젠 웹 접근성을 고려하고 생각하는게 즐겁다.
무늬만 개발자에서 진정한 개발자가 되어가고 있는 것 같아서 기쁘다.  <br/>
앞으로도 웹 접근성을 고려하며 정성이 있는 코드를 설계해보고 싶다.

<br/>
