### three.js的三个基本对象
1. sence;
2. camera;
3. renderer;

### 辅助库
1. stats: 检测出动画运行的帧频
2. dat.gui: 简化实验

### 材质
1. 基础材质不会对光源产生反应  *MeshBasicMaterial*
2. 对光源产生反应的材质 *MeshLambertMaterial*  和 *MeshPhongMaterial*
3. wireframe：框架

### 光源
1. SpotLight：会有锯齿状
2. PointLight: 少量锯齿状

### 动画 
1. requestAnimationFrame( *function* )方法: 可以指定一个函数，按照浏览器定义的时间间隔调用。可以在这个指定的函数里执行所有必要的绘画操作。
2. setMode()函数:a.若为0，则监测的是FPS(每秒显示的帧数);
                 b.若为1，则监测的是渲染时间。
3. 转动: rotation.x, rotation.y, rotation.z
4. gui.add()方法的功能和参数：
    a. 要添加的对象名称
    b. 已添加对象的属性
    c. 属性的取值范围
### ASCII效果（文本画）

### 问题???
1. renderer.setClearColorHex(0xEEEEEE);  //  报错
2. MeshLambertMaterial 设置之后颜色改变。但是依然镂空  
    解决方式：删除 wireframe：true 属性
3. 阴影的形状是块状
    解决方式：将原本用stoplight()创建的光源，改用PointLight()函数创建
4. page15-page16不知道是什么意思？
5. 错误一：renderScene()的执行应该在所有变量的定义之后
6. three05.html 使用ASCII效果时，显示 *THREE.AsciiEffect is not a constructor*，为什么???


### 投影
Three.js的光源默认不会导致物体间的投影，打开投影需要执行以下几步：
1. 打开渲染器的地图阴影: renderer.shadowMapEnabled = true;
2. 启用光线的投影：light.castShadow = true;
3. 把模型设置为生成投影：mesh.castShadow = true;
4. 把模型设置为接收阴影：mesh.receiveShadow= true;