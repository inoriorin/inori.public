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
![image](https://github.com/inoriorin/inori.public/blob/main/image/1/%5B%201%20%5D%20notepad/image_002.png)
<br/>
<br/>
<br/>
 
.7 &emsp; Houdini 按材质分组（ マテリアルによって選択する ）
~~~
  7.1 - Geometry Spreadsheet 几何表格面板 - Primitives 基本属性
~~~
![image](https://github.com/inoriorin/inori.public/blob/main/image/1/%5B%201%20%5D%20notepad/image_003.png)
~~~
  7.2 - Group 组
~~~
![image](https://github.com/inoriorin/inori.public/blob/main/image/1/%5B%201%20%5D%20notepad/image_004.png)
<br/>
<br/>
<br/>

.8 &emsp; Unreal Niagara 获取摄像机位置（ Niagara でカメラ位置をもらえる ）
~~~
  8.1 - Camera Query - Camera Properties CPU/GPU
~~~
![image](https://github.com/inoriorin/inori.public/blob/main/image/1/%5B%201%20%5D%20notepad/image_005.png)
<br/>
<br/>
<br/>
 
.9 &emsp; Houdini to Unreal 顶点色（ houdini を unreal に導入したあと頂点カラーの設置 ）
~~~
  9.1 - Unreal顶点色需要转换空间
~~~
![image](https://github.com/inoriorin/inori.public/blob/main/image/1/%5B%201%20%5D%20notepad/image_006.png)
<br/>
<br/>
<br/>
 
.10 &emsp; Unreal Hlsl 声明函数
~~~
  10.1 - 
  https://ikrima.dev/ue4guide/graphics-development/shader-development/tips-tricks/
 
  // 声明一个 输出 所输入值+1 的值 的函数

  return 1 ;
 
  }
 
  float nyako (float x)
  {
  return x + 1 ; 
 
  // 此为函数节点 需要暴露名为函数名（nyako）的端口 add 于引用端
 
  float1 a = nyako(2) ;
 
  return a ;

~~~
<img src=https://github.com/inoriorin/inori.public/blob/main/image/1/%5B%201%20%5D%20notepad/image_008.png width=80% />
<br/>
<br/>
<br/>
 
.11 &emsp; Unreal Material 逆 Tonemapping
~~~
  11.1 - 通过手动逆运算参数，并不精准
  float3 A = (pow(Color,3)*3.4475) - (pow(Color,2)*2.7866)+(1.2281*Color-0.0056) ;
~~~
~~~
  11.2 - 通过虚幻提供的逆函数 精准
  // 需要提前include TonemapCommon头文件
  return 1 ; 
  }
 
  #include "/Engine/Private/TonemapCommon.ush"
 
  void aa1(){
 
  //然后再使用该函数
  return FilmToneMapInverse(col) ;
~~~
<br/>
<br/>
<br/>
 
.12 &emsp; Unreal HLSL SubUV
~~~
  12.1 - 
  //sub uv
 
  float2 A = float2 ( 1 , 1 ) / GridNum  ;
 
  float B = fmod ( floor ( Frame ) , GridNum.x ) ; 
  // 上述为 先将帧数向下归整，后求与序列横向分布数量的余数，目的为计算当前帧停留在横向第几格的位置
  // 该步骤可以如此理解 
  // 当横向分布数量为4时，0帧与4的余数为0，1帧与4的余数为1，2帧与4的余数为2，如此类推，第四帧归零 ( 是横向逐帧前进播放的过程 ）

  float C = floor ( A.x * floor ( Frame ) ) ;
  //上述计算目的为得出当前帧停留在纵向第几排的位置
  // 该步骤可以如此理解
  // 当横向分布数量为4时，1/4等于0.25，第1帧时与横向数量乘积为0.25，向下归整为0，处在第1排，第10帧时为2，处在第3排
 
  float2 D = A * ( uv + float2 ( B , C ) ) ;
  // 上述计算将UV缩放为序列每格的大小 并按更上述的计算进行偏移，实现播放
 
 
  float B1 = fmod ( floor ( Frame ) + 1 ,  GridNum.x ) ;
  float C1 = floor ( A.x * ( floor ( Frame ) + 1 ) )  ;
  float2 D2 =  A * ( uv + float2 ( B1 , C1 ) ) ; 
 
  uvblend = D2 ; //在单帧计算时读取下一帧进行两帧的混合
 
  nyalerp = frac ( Frame ) ;// 两帧混合时使用的lerp系数
 
  return D ;
~~~
<br/>
<br/>
<br/>
 
.13 &emsp; Houdini 模型ID排序
~~~
  13.1 - 基于对分离模型后合并 或 fuse 后，模型顶点ID顺序发生变化的情况思考
  将 ID 定义进新的属性
  int @newID ;
  @newID = @ptnum ;
  // @ptnum是point环境下 pointID，vertex环境下为vtxnum 
~~~
~~~
  13.2 - 上述步骤结束后，正常编辑模型，于编辑的末尾 使用 sort 重新排序模型顶点序号
~~~
![image](https://github.com/inoriorin/inori.public/blob/main/image/1/%5B%201%20%5D%20notepad/image_009.png)
<br/>
<br/>
<br/>
 
.14 &emsp; Unreal 随机函数
~~~
  14.1 - 以输入的值为随机种，输出随机值
  return frac ( sin ( dot ( a1 , float2 ( 13 , 78.2 ) ) ) * 43760 ) ;
~~~
~~~
  14.2 - 程序化纹理 参考
  https://twitter.com/cmzw_/status/1555071863897722880
  https://www.shadertoy.com/view/7ldyWn
~~~
![image](https://github.com/inoriorin/inori.public/blob/main/image/1/%5B%201%20%5D%20notepad/image_010.png)
<br/>
<br/>
<br/>
 
.15 &emsp; Unreal LinearSine 线性正弦
~~~
  15.1 - 
  float a = frac ( inputa + 0.25 ) ;
 
  return lerp ( a * 2 , ( 1 - a ) * 2 , floor ( a * 2  ) ) ;
~~~
<br/>
<br/>
<br/>
 
.16 &emsp; 三角函数 两制互化（ 三角関数 ）
~~~
  16.1 - 
  两制互化：
  360° = 2π rad , 即 1π rad = 180° 
 
  角度转弧度公式 ：rad = deg * π / 180
  弧度转角度公式 ：deg = rad * 180 / π
~~~
<br/>
<br/>
<br/>




