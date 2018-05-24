
### 光源
1. AmbientLight: 环境光，基础光源，它的颜色会被加载到整个场景和所有对象的当前颜色上。
    var ambientLight = new THREE.AmbientLight(new THREE.Color(0xffffff));
    scene.add(ambientLight);//将光源添加到 scene 中
    影响整个场景
    没有特定的来源
    不会影响阴影的生成
    不能作为场景中唯一的光源
2. PointLight：点光源，朝着所有方向都发射光线
    单点发光
    不产生阴影  
    color:光源颜色
    intensity：强度，光照的强度，默认为1
    distance：距离， 光照照射得到的距离，决定光可以照射多远
    position：光源所在的位置
    visible：可见性，如果为true，光源就会打开
    var pointColor = new THREE.Color(0xffffff);
    var pointLight = new THREE.PointLight(pointColor);
    pointLight.distance = 100;
    pointLight.intensity = 1;
    scene.add(pointLight);
3. SpotLight：聚光灯光源：类型台灯，天花板上的吊灯，手电筒等（制造产生阴影的几个步骤,让球体和方块将阴影投影到地上，哪些物体投射阴影，哪些物体接受阴影。）锥形效果
    制造阴影的步骤：
    render.shadowMapEnabled=true;  //告诉render我们需要阴影(允许阴影隐射)
    plane.receiveShadow=true;  //地面接受阴影
    cube.castShadow=true;  //cast投射，就是方块投射阴影
    spotLight.castShadow=true;  //不是所有的光源都可以投射阴影 ,这里使用聚点光源可以产生阴影
    特有属性：
    a. *target*    光源的指向
    b. *distance*    光锥的长度
    c. *angle*    光锥的宽度
    d. *exponent*    指定光强以多快的速度从中心开始衰减，exponent越大，离中心越远光强衰减的越快 
    var pointColor = new THREE.Color(0xffffff);
    var spotLight = new THREE.SpotLight(pointColor);
    spotLight.position.set(-40, 60, -10);
    spotLight.castShadow = true;
    spotLight.shadowCameraNear = 2;
    spotLight.shadowCameraFar = 200;
    spotLight.shadowCameraFov = 30;
    spotLight.target = plane;//光照照向地面
    spotLight.distance = 0;
    spotLight.angle = 0.4;
    scene.add(spotLight);
    shadowCameraVisible = true;    // 03-spot-light+directiveLight 中的debug。
4. DirectionalLight：方向光，又称无限光，从这个发出的光源可以看做是平行光.
    var pointColor = new THREE.Color(0xffffff);
    var directionalLight = new THREE.DirectionalLight(pointColor);
    directionalLight.position.set(-40, 60, -10);
    directionalLight.castShadow = true;
    directionalLight.shadowCameraNear = 2;
    directionalLight.shadowCameraFar = 200;
    directionalLight.shadowCameraLeft = -50;
    directionalLight.shadowCameraRight = 50;
    directionalLight.shadowCameraTop = 50;
    directionalLight.shadowCameraBottom = -50;
    directionalLight.distance = 0;
    directionalLight.intensity = 0.5;
    directionalLight.shadowMapHeight = 1024;
    directionalLight.shadowMapWidth = 1024;
    scene.add(directionalLight);
    平行光
    所有对象接收的光强都是一样的
    会产生阴影
    与聚点光源的主要差别是：聚点光源光距离目标越远光越暗淡，而平行光光强都是一样的。
    只用 direction (方向)，color (颜色)，intensity (强度)来计算属性和阴影
    -形成的不是光锥而是一个方块（很重要）   
5. HemisphereLight 半球光源  一种特殊光源，可以用来创建更加自然的室外光线，模拟反光面和光线微弱的天空
    var hemiLight = new THREE.HemisphereLight(0x0000ff, 0x00ff00, 0.6);
6. AreaLight 面光源  可以指定散发光源的平面，而不是空间中的一个点
    var areaLight1 = new THREE.AreaLight(0xff0000, 3);
7. LensFlare  镜头眩光 不是一种光源，但是可以利用LensFlare为场景中的光源添加眩光效果
    var lensFlare = new THREE.LensFlare(textureFlare0, 350, 0.5, THREE.AdditiveBlending, flareColor);



### 阴影
1. THREE.BasicShadowMap：普通阴影映射
2. THREE.PCFShadowMap：柔化边缘的阴影映射
3. THREE.PCFSoftShadowMap：柔化边缘的软阴影映射


### THREE.Color() 对象
1. renderer.setClearColor(new THREE.Color( 0xeeeeee));
2.  gui.addColor(controls, 'ambientColor').onChange(function(e){
        ambientLight.color = new THREE.Color(e)
    });


### THREE.js中用到的方法
1. THREE.ImageUtils.loadTexture()函数已被丢弃，请使用THREE.TextureLoader().load()函数。
2. 贴图（使用图片）的3D模型需要不断渲染才能显示。（只贴颜色的则不需要，实验所得，仅供参考）。
3. 渲染方法如下： (javascript) 
    function run(){ 
        renderer.render(scene.camera); 
        requestAnimationFrame(run); 
    } 
4. THREE.Object3D() *光源*指向空间中任意一点（代码实现如下）
    var target = new THREE.Object3D(); 
    target.position = new THREE.Vector3(5, 0, 0);




### 问题
1. 03-spot-light 中光是锯齿状？？？    
