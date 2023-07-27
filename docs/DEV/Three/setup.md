# First app by Three.js

Create a new folder.

Run commands `npm install --save three` and `npm install --save-dev vite` to get `package.json` like:

```json
{
  "devDependencies": {
    "vite": "^4.4.7"
  },
  "dependencies": {
    "three": "^0.154.0"
  }
}
```

Create file `index.html`:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>Rotating Cube</title>
    <style>
      body {
        margin: 0;
      }
    </style>
  </head>
  <body>
    <script type="module" src="./main.js"></script>
  </body>
</html>
```

Create file `main.js`:

```js
import * as THREE from "three";

const scene = new THREE.Scene();

const geometry = new THREE.BoxGeometry(1, 1, 1);
const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
const cube = new THREE.Mesh(geometry, material);
scene.add(cube);

const camera = new THREE.PerspectiveCamera(
  75,
  window.innerWidth / window.innerHeight,
  0.1,
  1000
);
camera.position.z = 3;

const renderer = new THREE.WebGLRenderer();
renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);

function animate() {
  requestAnimationFrame(animate);
  renderer.render(scene, camera);
  cube.rotation.y += 0.01;
}
animate();
```

Use `npx vite` to check the app in the browser.

Use `npx vite build` to build the app.

## Bonus

### .gitignore

```
node_modules/
dist/
```

### Ckeck WebGL compatibility

```js
import WebGL from "three/addons/capabilities/WebGL.js";

if (WebGL.isWebGLAvailable()) {
  // Initiate function or other initializations here
  animate();
} else {
  const warning = WebGL.getWebGLErrorMessage();
  document.getElementById("container").appendChild(warning);
}
```

## References

- https://threejs.org/docs/#manual/en/introduction/Installation
- https://threejs.org/docs/#manual/en/introduction/Creating-a-scene
- https://threejs.org/docs/#manual/en/introduction/WebGL-compatibility-check
