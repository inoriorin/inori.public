.1 &emsp; houdini 法线传递（ 丸になるの法線設置 ）<br/>
~~~
  1.1 - 使用vex语言 为模型设置法线
  @N = v@opinput1_N ; 
  // v@opinput1_ 代表引用此节点的第二个输入端 N代表法线 意为输出使用第二输入端的法线的第一输入端
 
  @N = normalize(@P - set(0,0,0)) ;
  // normalize为归一化 P为点的位置 注意 vex中直接使用某值或为某值赋值时 要使用 set 格式
~~~
~~~
  1.2 - 使用 ray 节点 按最近距离传递属性
  Ray ：射线节点 将A平面投影至B平面
  Point Intersection Normal : A面延法线射线后求至B面的交点处法线信息 （将该交点法线信息传递回A）
~~~
![image](https://github.com/inoriorin/inori.public/blob/main/image/1/%5B%201%20%5D%20notepad/image_001.png)
<br/>
<br/>
<br/>

.2 &emsp; Blender 载入MMD PMX模型（ PMD のキャラを blender に読み込む ）<br/>
~~~
  2.1 - github - Blender MMDtools 插件
  https://github.com/UuuNyaa/blender_mmd_tools
~~~
<br/>
<br/>
<br/>

.3 &emsp; Unreal 高光公式 非各向异性
~~~
  3.1 - 
  float3 L = LightVector ;
  float3 V = CameraVector ;
  float3 N = VertexNormal ;
  float3 H = normalize(lerp(L,V,0.5)); // 为光源方向与视线方向的半角向量
  float1 Specular = dot(N,H) ;
~~~
<br/>
<br/>
<br/>

.4 &emsp; Houdini 模型平滑后仍有断面问题（ メッシュの頂点縫合 ）
~~~
  4.1 - 模型本身含有断点 导入Houdini后断点的情况下做平滑不会处理断点部分 需执行 fuse 缝合
~~~
<br/>
<br/>
<br/>
 
.5 &emsp; houdini 坐标系（ houdini を unreal に導入したあと座標系の転換 ）
~~~
  5.1 - Houdini坐标系与Unreal坐标系中 Y轴与Z轴是相反的 故在输出后要进行Y轴与Z轴的对调
~~~
<br/>
<br/>
<br/>
 
.6 &emsp; Unreal Niagara 粒子系统整体位置移动（ Niagarae particle 全体移動 ）
~~~
  6.1 - System Location 模块
~~~
<br/>
<br/>
<br/>
 


