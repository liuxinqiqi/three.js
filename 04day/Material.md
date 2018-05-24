### 材质
1. MeshBasicMaterial：对光照无感，给几何体一种简单的颜色或显示线框。
    var meshMaterial = new THREE.MeshBasicMaterial({color: 0x7777ff});
2. MeshLambertMaterial：这种材质对光照有反应，用于创建暗淡的不发光的物体。
3. MeshPhongMaterial：这种材质对光照也有反应，用于创建金属类明亮的物体。

4. MeshDepthMaterial: 网格深度材质 
    外观由物体到相机的距离决定的
    var scene = new THREE.Scene();
    scene.overrideMaterial = new THREE.MeshDepthMaterial();  
5. MeshNormalMaterial: 网格法向材质
6. ShaderMaterial: 着色器材质
7. LineBasicMaterial: 直线基础材质
8. LineDashedMaterial: 虚线材质
9. 联合材质 
    var cubeGeometry = new THREE.BoxGeometry(cubeSize, cubeSize, cubeSize);
    // 1. 新材质
    var cubeMaterial = new THREE.MeshDepthMaterial();
    // 2. （1）transparent设置为true
    //    （2）指定融合模式
    var colorMaterial = new THREE.MeshBasicMaterial({
        color: controls.color, 
        transparent: true, 
        blending: THREE.MultiplyBlending
    });
    // 3. createMultiMaterialObject() 函数创建一个网格的时候，几何体会被复制，返回一个网格组，里面的两个网格完全相同 
    var cube = new THREE.SceneUtils.createMultiMaterialObject(cubeGeometry, [colorMaterial, cubeMaterial]);
    // 4. 如果没有最后一行，渲染时画面会有闪烁，因为他们会直接在彼此的上面渲染，通过缩小带有MeshDepthMaterial材质的网格，就可以避免这种现象。
    cube.children[1].scale.set(0.99, 0.99, 0.99);
    // var cube = new THREE.Mesh(cubeGeometry, cubeMaterial);
    cube.castShadow = true;    


### 问题
1. 03Combined 无法移除cube？？？