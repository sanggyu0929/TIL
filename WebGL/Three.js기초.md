## Three.js 소개 
> [Three.js](http://threejs.org)는 간단히 말하면 Javascript 3D library이다.  
> WebGL 기술을 기반으로 렌더링과 카메라,   
> 조명등의 3D 프로그래밍 기술을 간단하게 사용할 수 있도록 제공한 라이브러리이다.

* [Renderer](https://threejs.org/docs/#api/en/constants/Renderer)
> Three.js의 핵심 객체.  
> [Scene](https://threejs.org/docs/#api/en/scenes/Scene)과 [Camera](https://threejs.org/docs/#api/en/cameras/Camera) 객체를 넘겨 받아 3D 씬의 일부를 평면(2차원) 이미지로 렌더링한다.

* [Mesh](https://threejs.org/docs/#api/en/objects/Mesh)
> 어떤 [Material](https://threejs.org/docs/#api/en/materials/Material) 하나의 [Geometry](https://threejsfundamentals.org/threejs/lessons/threejs-custom-geometry.html)를 그리는 객체이다.  
> `Material`,`Geometry`는 재사용이 가능하여 여러개의 `Mesh`가 하나의 `Material` 또는 `Geometry`를 동시에 참조할 수 있다.

* [Material](https://threejs.org/docs/#api/en/materials/Material)  
> 기하학 객체를 그리는 데 사용하는 [표면 속성](https://threejsfundamentals.org/threejs/lessons/threejs-materials.html)이다.  
> 색이나 밝기를 지정할 수 있다.  
> 기하학 객체의 표면을 이미지로 덮어씌울 때 주로 사용.

* [Geometry](https://threejsfundamentals.org/threejs/lessons/threejs-custom-geometry.html)  
> 기하학 객체의 정점 데이터이다. [ex : 구(sphere), 정육면체(cube), 면(plane)...]  
> 기하학 객체를 직접 만들 수도, 불러올 수도 있다.

* [Texture](https://threejs.org/docs/#api/en/textures/Texture)  
> 이미지나 파일에서 로드한 이미지, canvas로 생성한 이미지 또는 다른 `Scene` 객체에서 렌더링한 결과물이다.

* [Light](https://threejs.org/docs/#api/en/lights/Light)  
> 여러 종류의 광원에 해당한다.

## Reference
> https://threejsfundamentals.org/threejs/lessons/threejs-fundamentals.html