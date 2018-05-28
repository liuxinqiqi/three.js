### 粒子（THREE.ParticleBasicMaterial({})） 创建和设计粒子
1. THREE.Particles(material)  需要传入的参数是材质。它和THREE.Mesh一样，都是THREE.Object3D对象的扩展。
（1）ParticleBasicMaterial （去除）
（2）ParticleProgramMaterial （去除）
2. 渲染器一般用的是CanvasRenderer，因为创建粒子并且直接添加到场景中只对CanvasRenderer有效。
    渲染器如果是WebGLRenderer，首先要创建一个THREE.ParticleSystem对象，然后通过这个对象来创建粒子。？？？？？？？可是01的例子里面用的是WebGLRenderer，可以通用了？（不必了，可以直接用SpriteMaterial或者PointCloudMaterial创建材质）
3. CanvasRenderer和WebGLRenderer的比较和区别？??
4. 已经没有// var material = new THREE.ParticleBasicMaterial();  --->pointMaterial代替
          // var material = new THREE.ParticleProgramMaterial(); 
    这两中material了么？？？？（已经去掉了）
5. scene.getObjectByName("particles") 获取name是particles的元素
6. color.setHSL()  值在0 - 1之间
7. SpriteMaterial( parameters )
    parameters -- 定义默认属性的对象
    color - sprite的颜色。
    map - 纹理贴图
    rotation - sprite的旋转
    fog - 是否使用场景雾。
8. Sprite( material )
    material — 材料(Material) 的一个实例(可选)。
    This 创建一个新的 sprite with an specific material.
9. 在WebGLRenderer()中使用html5画布的时候，需要添加一些代码
（1）var canvas = document.createElement('canvas');
    canvas.width = 32;
    canvas.height = 32;
    var ctx = canvas.getContext('2d');
（2）var texture = new THREE.Texture(canvas);
    texture.needsUpdate = true;
    return texture;
10. sizeAttenuation  指明粒子大小是否随距离而变。默认为true。
11. map: getTexture(), // 为粒子加载纹理



### 粒子的属性
1. color
2. map
3. size
4. sizeAnnutation
5. vetexColor
6. opacity
7. transparent
8. blending
9. fog



### CanvasRenderer
1. color
2. program
3. opacity
4. transparent
5. blending




### 粒子系统（THREE.ParticleSystem(geom, material)）创建一个粒子集合



### 精灵（Sprite）
1. color
2. map
3. sizeAnnutation
4. opacity;
5. blending
6. fog;
7. useScreenCoordinates
8. scaleByViewport
9. alignment
10. uvOffset
11. uvScale

### 加载外部图片
1. THREE.ImageLoader.load ( url, onLoad, onProgress, onError )
    url — 资源链接，必选参数。
    onLoad — 当加载完成时被调用。参数将是已加载的 image。
    onProgress — 当加载在进行中时被调用。参数是 XmlHttpRequest 实例，包含 .total 和 .loaded 字节。
    onError — 如果加载有错误将调用该函数。
2. 去除纹理上的黑色背景(1)：
   THREE.AdditiveBlending：在画新像素时，背景像素的颜
色会被添加到新像素上。（或者将纹理中的黑色定义成透明的？？？？？）
3. 使用纹理格式化粒子（去除纹理的黑色背景(2)）
   （1）depthTest: false 设置材质是深度测试设置为false后就好了 
   （2）depthWrite: false 这个属性决定这个对象是否影响WebGL的深度缓存，设置为false，保证各个粒子系统之间互不影响




### 注意
1. vertexColors：通常情况下所有粒子具有相同的颜色，如果该属性为true，而且几何体的color数组也有值，那就使用颜色数组中的值。，默认是false。
2. sizeAttenuation：启用/禁用随距离而发生尺寸衰减。
3. SpriteCanvasMaterial：精灵画布材料   

4.  CanvasRenderer  --> THREE.Particle
    WebGLRenderer  --> THREE.Sprite
    创建大量粒子（同一材质）：THREE.ParticleSystem(几何体中的每个顶点会被渲染成粒子，并使用指定的材质)
5. map: 使用图片或者html5的画布来格式化粒子
6. 改变粒子的位置他们可以动起来
7. useScreenCoordinates: true; 对象在屏幕上绝对定位
