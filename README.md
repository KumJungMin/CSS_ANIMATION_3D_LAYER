# hover시 3d로 변하는 이미지 레이어

## 1. preview

### hover, position, opacity, tranform 사용

<img src="https://j.gifs.com/vlB9Pn.gif" />


## 2. 코드 분석

### 1) html

#### (1) div안에 똑같은 크기의 이미지를 배치
- `container클래스` : `body`상에서 수직, 수평 중앙정렬
- `app-ui 클래스` : 크기값이 같은 이미지들, 애니메이션은 `rotate`형태로 진행


```html
<body>
    <div class="container">   
        <div class="app-ui"> 
            <img src="./img/app-ui-01.jpg"/>
            <img src="./img/app-ui-02.jpg"/>
            <img src="./img/app-ui-03.jpg"/>
            <img src="./img/app-ui-04.jpg"/> 
        </div>

    </div>
<body>

```

<br/><br/>

### 2) css

#### (1) 중앙 정렬하기
- 요소를 수직, 수평 중앙 정렬하는 방법에는 2가지가 있다.
            
```css
/* 해당 요소를 수직, 수평 중앙하는 방법(1) */
.container{
    position: absolute;
    top: 50%;
    left : 50%;
    transform: translate(-50%, -50%);
    }
    
/* body에 적용하여 body 내부요소를 수직, 수평 중앙하는 방법(2)     
body{ 
     display : flex;
     justify-content: center;  수평중앙
     align-items : center;     수직중앙
     height : 100vh;
    }
    */
```

<br/>

#### (2) 이미지들을 담은 app-ui태그 설정
- `app-ui` 크기 

  : `app-ui`의 크기를 이미지와 같게 한다.

<br/>

- 누운 것처럼 변형 

  : `transform`을 이용해 이미지가 누운 것처럼 변형한다.
  
  : `rotate`를 주고, `skewX`를 준다.(`skewX`는 요소를 주어진 각도만큼 x축 방향으로 기울임)
  
  : 이미지들의 부모요소인 `app-ui`를 기울였으니, 이제 내부 요소들도 자동으로 기울어짐
  
  : `scale`는 크기를 0.7배로 한다.
  
```css

.app-ui{
    /* width, height는 이미지 사이즈와 같게 */
    width: 340px;
    height : 640px;

    /* 사진을 누워있는 것처럼 표현하기 */
    transform: rotate(-30deg) skewX(20deg) scale(0.7);   
   
    /*이미지들을 화면의 동적 변화에도 같은 위치에 두기 위해 부모는 상대위치로 둠*/
    /*부모의 자식들을 절대위치로 주어, top, left 위치를 조정하면 됨*/
    position: relative;  

    box-shadow: 0 0 20px rgba(0,0,0,0.3);   /*그림자를 줌(1)*/
    transition: 0.5s;                       /*그림자를 줌+0.5초 효과*/

    /*백그라운드를 연한 회색을 주어, 이미지와 부모요소간의 부자연스러운 공백을 줄임*/
    background-color: #eee;               

}

.app-ui:hover{
    /*그림자를 줌+0.5초 효과+hover시 넓은 영역까지 그림자생김*/
    /* x, y, 퍼짐정도 */
    box-shadow: -50px 100px 60px rgba(0,0,0,0.3); 
    
}

```


<br/>

#### (3)  img별 애니메이션 설정
- 4개의 이미지들을 처음에는 겹치게 둔다.
- `app-ui`에 `hover`시 이미지별로 다른 애니메이션을 준다.
- 이미지에는 위치값이 변경되는 애니메이션을 적용한다.
 
 
```css
.app-ui img{
    /* 이미지들을 같은 위치에 두고, hover시 보이게 한다. */
    position: absolute;  /*이미지들을 같은 위치에 두기 위해 절대위치로 둠(1)*/
    transition: 0.5s;    
    /*이미지에 이벤트가 발생하여 0.5초 동안 자연스럽게 발생할거야
    요소자체에 transition을 써야함, hover한 곳에 쓰면 x
    */
}


/* app-ui에 hover시 -> 내부 이미지요소별로 다른 애니메이션을 줌 */
.app-ui:hover img:nth-child(1) {
/* transform은 변형 > translate는 이동(x,y축 둘다 적어야함)*/
    transform: translate(40px, -40px) ;
    opacity: 0.2;  /*투명도를 이용해, hover시 이미지간 구별을 준다.*/
}
.app-ui:hover img:nth-child(2) {
    /* 40px만큼 갭을 준다. */
    transform: translate(80px, -80px) ;
    opacity: 0.4;
}
.app-ui:hover img:nth-child(3) {
    /* 40px만큼 갭을 준다. */
    transform: translate(120px, -120px) ;
    opacity: 0.6;
}
.app-ui:hover img:nth-child(4) {
    /* 40px만큼 갭을 준다. */
    transform: translate(160px, -160px) ;
}
    
```

