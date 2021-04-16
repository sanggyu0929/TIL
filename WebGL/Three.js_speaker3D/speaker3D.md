## Three.js를 사용하여 3D speaker 모형 만들기

- index.html

```html
<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Hi Class</title>
    <link rel="stylesheet" href="./src/css/style.css" />
  </head>
  <body>
    <div class="speakerBox">
      <canvas id="myCanvas"></canvas>
    </div>
    <script type="module" src="./src/js/script.js"></script>
  </body>
</html>
```

- style.css

```css
* {
  margin: 0;
  padding: 0;
  outline: 0;
}

html {
  width: 100%;
  height: 100%;
}

body {
  width: 100%;
  height: 100%;
  overflow: hidden;
}

.speakerBox {
  width: 100%;
  height: 100%;
  background: radial-gradient(
    circle at 70%,
    rgba(34, 34, 34, 0.6),
    #222 30%,
    #222 75%
  );
}

.speakerBox > canvas {
  width: 100%;
  height: 100%;
}
```

- script.js

```js
import * as THREE from "https://threejsfundamentals.org/threejs/resources/threejs/r125/build/three.module.js";

function main() {
  const canvas = document.querySelector("#myCanvas");
  const gl = canvas.getContext("webgl");
  gl.clearColor(0.0, 0.5, 0.0, 1.0);

  const renderer = new THREE.WebGLRenderer({ canvas });
  const fov = 35;
  const aspect = 2;
  const near = 1.1;
  const far = 100;
  const camera = new THREE.PerspectiveCamera(fov, aspect, near, far);
  camera.position.z = 4;

  const scene = new THREE.Scene();

  {
    const color = 0xffffff;
    const intensity = 1;
    const light = new THREE.DirectionalLight(color, intensity);
    light.position.set(0.0, 0.0, 1.0);
    scene.add(light);
  }

  const boxWidth = 2;
  const boxHeight = 1;
  const boxDepth = 0.8;
  const geometry = new THREE.BoxGeometry(boxWidth, boxHeight, boxDepth);
  const cubes = [];
  const loader = new THREE.TextureLoader();
  const materials = [
    new THREE.MeshBasicMaterial({
      map: loader.load("./src/img/speakerSide.png"),
    }),
    new THREE.MeshBasicMaterial({
      map: loader.load("./src/img/speakerSide.png"),
    }),
    new THREE.MeshBasicMaterial({
      map: loader.load("./src/img/speakerTop.png"),
    }),
    new THREE.MeshBasicMaterial({
      map: loader.load("./src/img/speakerBottom.png"),
    }),
    new THREE.MeshBasicMaterial({
      map: loader.load("./src/img/speakerFront.png"),
    }),
    new THREE.MeshBasicMaterial({
      map: loader.load("./src/img/speakerBack.png"),
    }),
  ];

  const cube = new THREE.Mesh(geometry, materials);
  scene.add(cube);
  cubes.push(cube);

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

  function render() {
    if (resizeRendererToDisplaySize(renderer)) {
      const canvas = renderer.domElement;
      camera.aspect = canvas.clientWidth / canvas.clientHeight;
      camera.updateProjectionMatrix();
    }
    cube.rotation.x += 0.005;
    cube.rotation.y += 0.005;

    renderer.render(scene, camera);
    requestAnimationFrame(render);
  }
  requestAnimationFrame(render);
}

main();
```
