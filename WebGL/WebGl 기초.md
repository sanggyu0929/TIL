# WebGL 기초

## WebGL이란?

> 웹 기반의 그래픽 라이브러리이다.  
> 3차원 그래픽을 사용하기 위한 프로그래밍 인터페이스를 제공한다.  
> HTML5 캔버스 요소를 사용하고 [문서 객체 모델](https://ko.wikipedia.org/wiki/%EB%AC%B8%EC%84%9C_%EA%B0%9D%EC%B2%B4_%EB%AA%A8%EB%8D%B8) 인터페이스를 사용해서 액세스할 수 있다.

## 지원 브라우저

<div class="imgContainer" style="display : flex;">
    <div class="imgBox" style="width: 100%; height : 100%; margin : 10px;">
        <img src="https://upload.wikimedia.org/wikipedia/commons/a/a5/Google_Chrome_icon_%28September_2014%29.svg" width='100'>
        <span style="display : block; text-align : center;">Google Chrome 9 이상<span>
    </div>
    <div class="imgBox" style="width: 100%; height : 100%; margin : 10px;">
        <img src="https://upload.wikimedia.org/wikipedia/commons/d/d2/Firefox_Logo%2C_2017.png" width='100'>
        <span style="display : block; text-align : center;">Firefox 4 이상<span>
    </div>
    <div class="imgBox" style="width: 100%; height : 100%; margin : 10px;">
        <img src="https://upload.wikimedia.org/wikipedia/commons/4/49/Opera_2015_icon.svg" width='100'>
        <span style="display : block; text-align : center;">Opera 15 이상<span>
    </div>
    <div class="imgBox" style="width: 100%; height : 100%; margin : 10px;">
        <img src="https://upload.wikimedia.org/wikipedia/commons/9/97/Microsoft_Edge_Logo.svg" width='100'>
        <span style="display : block; text-align : center;">Microsoft Edge<span>
    </div>
</div>


## WebGL 설정 및 설치 

> WebGL zip 다운로드 링크 https://github.com/gfxfundamentals/webgl-fundamentals.git

## 웹 서버 사용

### 방법 1 
> [Servez](https://greggman.github.io/servez/)

### 방법 2 
> npm을 통한 install  
1.  ```npm -g install servez``` OS X를 사용할 경우 ```sudo npm -g install servez```
2. ```servez path/to/folder/where/you/unzipped/files```<br>*만약 path를 지정하지 않으면 servez가 현재 폴더를 serve할 것이다.*
3. 브라우저에서 `http://localhost:8080/webgl-fundamentals-master/webgl/`으로 접속하여 사용 예시를 볼 수 있다.
![예시](https://webglfundamentals.org/webgl/lessons/resources/chrome-devtools.png)










