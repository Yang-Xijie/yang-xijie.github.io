# USDZ

[SIGGRAPH 23 Course | USD in Production](https://dl.acm.org/doi/10.1145/3587423.3595531)

个人感觉对于研究来说好像没什么帮助……

---

## 相关

- AR Quick Look https://developer.apple.com/augmented-reality/quick-look/
    - 苹果官方推荐使用的模型基本上都是 USDZ
- Reality Converter https://developer.apple.com/augmented-reality/tools/
    - convert common 3D file formats (.obj, .gltf) to USDZ
- https://openusd.org/release/index.html
    - https://openusd.org/release/spec_usdz.html
    - https://openusd.org/release/usdfaq.html

## 解压

https://developer.apple.com/augmented-reality/quick-look/ 中给出的松饼的 .usdz 文件，解压后得到：

```
.
├── pancakes
│   ├── 0
│   │   ├── blueberry_bc.png
│   │   ├── blueberry_n.png
│   │   ├── blueberry_r.png
│   │   ├── pancakes_bc.png
│   │   ├── pancakes_n.png
│   │   ├── pancakes_r.png
│   │   ├── plate_ao.png
│   │   ├── walnuts_bc.png
│   │   ├── walnuts_n.png
│   │   └── walnuts_r.png
│   └── pancakes.usdc
└── pancakes.usdz
```

## Blender

Universal Scene Description (`.usd*`)
