## Three.js의 텍스처(Textures)

### Texture
> 텍스처는 일반적으로 포토샵 같은 3rd party 프로그램으로 만들어진 이미지이다.

### TextureLoader
 ``` js
 const texture = new THREE.TextureLoader().load( 'path/img/url' );
const material = new THREE.MeshBasicMaterial( { map: texture } ); 
```

### 육면체 면에 텍스처 삽입
HTML
``` html
<canvas id="myCanvas"></canvas>
```
CSS
``` css 
* {
    margin: 0;
    padding: 0;
    outline : 0;
}
html, body {
    width:100%;
    height: 100%;
}
#myCanvas {
    width: 100%;
    height: 100%;
    display: block;
}
```

Js
``` js
import * as THREE from 'https://threejsfundamentals.org/threejs/resources/threejs/r125/build/three.module.js';

function main() {
  const canvas = document.querySelector('#myCanvas');
  const renderer = new THREE.WebGLRenderer({canvas});

  const fov = 75;
  const aspect = 2;  // the canvas default
  const near = 0.1;
  const far = 5;
  const camera = new THREE.PerspectiveCamera(fov, aspect, near, far);
  camera.position.z = 2;

  const scene = new THREE.Scene();

  const boxWidth = 1;
  const boxHeight = 1;
  const boxDepth = 1;
  const geometry = new THREE.BoxGeometry(boxWidth, boxHeight, boxDepth);

  const cubes = [];  // just an array we can use to rotate the cubes
  const loader = new THREE.TextureLoader();

  const material = new THREE.MeshBasicMaterial({
    map: loader.load('https://threejsfundamentals.org/threejs/resources/images/wall.jpg'),
  });
  const cube = new THREE.Mesh(geometry, material);
  scene.add(cube);
  cubes.push(cube);  // add to our list of cubes to rotate

  function resizeRendererToDisplaySize(renderer) {
    const canvas = renderer.domElement;
    const width = canvas.clientWidth;
    const height = canvas.clientHeight;
    const needResize = canvas.width !== width || canvas.height !== height;
    if (needResize) {
      renderer.setSize(width, height, false);
    }
    return needResize;
  }

  function render(time) {
    time *= 0.001;

    if (resizeRendererToDisplaySize(renderer)) {
      const canvas = renderer.domElement;
      camera.aspect = canvas.clientWidth / canvas.clientHeight;
      camera.updateProjectionMatrix();
    }

    cubes.forEach((cube, ndx) => {
      const speed = .2 + ndx * .1;
      const rot = time * speed;
      cube.rotation.x = rot;
      cube.rotation.y = rot;
    });

    renderer.render(scene, camera);

    requestAnimationFrame(render);
  }

  requestAnimationFrame(render);
}

main();
```

## Reference
https://threejs.org/docs/#api/en/loaders/TextureLoader  
https://threejsfundamentals.org/threejs/lessons/threejs-textures.html
