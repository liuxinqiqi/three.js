### 材质
1. MeshBasicMaterial：对光照无感，给几何体一种简单的颜色或显示线框。
    a. var meshMaterial = new THREE.MeshBasicMaterial({color: 0x7777ff});
    b. shading : 着色，可选值是FlatShading 和 SmoothShading
2. MeshLambertMaterial：这种材质对光照有反应，用于创建暗淡的不发光的物体。
    var meshMaterial = new THREE.MeshLambertMaterial({color: 0x7777ff});
3. MeshPhongMaterial：这种材质对光照也有反应，用于创建金属类明亮的物体。
    var meshMaterial = new THREE.MeshPhongMaterial({color: 0x7777ff});
4. MeshDepthMaterial: 网格深度材质 
    外观由物体到相机的距离决定的
    var scene = new THREE.Scene();
    scene.overrideMaterial = new THREE.MeshDepthMaterial();  
5. MeshNormalMaterial: 网格法向材质
    var meshMaterial = new THREE.MeshNormalMaterial({color: 0x7777ff});
    shading : 着色，可选值是FlatShading 和 SmoothShading
6. ShaderMaterial: 着色器材质  (第九章，第十一章)




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
10. MeshFaceMaterial 材质容器   为每个面指定



### 注意点
1. 材质不是都会被光照影响
    MeshLambertMaterial, MeshPhongMaterial计算光照影响
2. opacity属性必须通过transparent=true;结合才能使用
3. 材质的大部分属性在运行时可以修改，但是有一些不可以（eg: size）, 如果要修改，将needsUpdate设置为true；
4. 为一个几何体赋予多种材质会复制几何体，从而创建出多个网格（这里的网格指的是mesh？？）；
5. three.line对象不可以用普通材质覆盖，只可以用LineBasicMaterial和LineDashedMaterial，而且使用LineDashedMaterisl的时候必须

### 问题
1. 03Combined 无法移除cube？？？
2. CanvasRenderer 和 WebGLRender对象的区别？？？
3. needsUpdate 是把所有的材质都改变了么？？？
    needsUpdate  是否刷新， 值为true的时候，会使用新的材质属性刷新它的缓存 
4.  renderer.shadowMapEnabled = true; 
    renderer.shadowMapEnabled = false;  的区别？？？  meshfacematerial 
5. scene中的children一起旋转
6. 少一个着色器。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。（记得补看）