
### 光源
1. AmbientLight: 环境光，基础光源，它的颜色会被加载到整个场景和所有对象的当前颜色上。
    影响整个场景
    没有特定的来源
    不会影响阴影的生成
    不能作为场景中唯一的光源
2. PointLight：点光源，朝着所有方向都发射光线
    单点发光
    不产生阴影
3. SpotLight：聚光灯光源：类型台灯，天花板上的吊灯，手电筒等（制造产生阴影的几个步骤,让球体和方块将阴影投影到地上，哪些物体投射阴影，哪些物体接受阴影。）锥形效果
    制造阴影的步骤：
    render.shadowMapEnabled=true;//告诉render我们需要阴影(允许阴影隐射)
    plane.receiveShadow=true;//地面接受阴影
    cube.castShadow=true;//cast投射，就是方块投射阴影
    spotLight.castShadow=true;//不是所有的光源都可以投射阴影 ,这里使用聚点光源可以产生阴影
    特有属性：
    a. *target*    光源的指向
    b. *distance*    光锥的长度
    c. *angle*    光锥的宽度
    d. *exponent*    指定光强以多快的速度从中心开始衰减，exponent越大，离中心越远光强衰减的越快 
4. DirectionalLight：方向光，又称无限光，从这个发出的光源可以看做是平行光.
    平行光
    所有对象接收的光强都是一样的
    会产生阴影
    与聚点光源的主要差别是：聚点光源光距离目标越远光越暗淡，而平行光光强都是一样的。
    只用 direction (方向)，color (颜色)，intensity (强度)来计算属性和阴影
    -形成的不是光锥而是一个方块（很重要）   
5. HemisphereLight 半球光源  一种特殊光源，可以用来创建更加自然的室外光线，模拟反光面和光线微弱的天空
6. AreaLight 面光源  可以指定散发光源的平面，而不是空间中的一个点
7. LensFlare  镜头眩光 不是一种光源，但是可以利用LensFlare为场景中的光源添加眩光效果

### 阴影
1. THREE.BasicShadowMap：普通阴影映射
2. THREE.PCFShadowMap：柔化边缘的阴影映射
3. THREE.PCFSoftShadowMap：柔化边缘的软阴影映射


### THREE.Color() 对象
1. renderer.setClearColor(new THREE.Color( 0xeeeeee));
2.  gui.addColor(controls, 'ambientColor').onChange(function(e){
        ambientLight.color = new THREE.Color(e)
    });