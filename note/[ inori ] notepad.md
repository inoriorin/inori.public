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
  1.1 - github - Blender MMDtools 插件
  https://github.com/UuuNyaa/blender_mmd_tools
~~~

