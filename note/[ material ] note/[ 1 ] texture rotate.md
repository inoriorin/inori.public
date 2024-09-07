```
已知长度为 1 的向量 n = ( x , y ) ; n 以 ( 0 , 0 ) 为中心逆时针旋转 a1 度 得到 v ( x , y ) ; 推算 v ( x , y )

正余弦公式：
sin∠A = 对 / 斜 ； cos∠A = 邻 / 斜
 
两角和公式：
sin(∠A + ∠B) = sin∠A * cos∠B + cos∠A * sin∠B
cos(∠A + ∠B) = cos∠A * cos∠B - sin∠A * sin∠B

v.x = cos ( a1 + a2 ) = cos (a1) * cos (a2) - sin (a1) * sin (a2) = cos (a1) * x - sin (a1) * y ;
v.x = sin ( a1 + a2 ) = sin (a1) * cos (a2) + cos (a1) * sin (a2) = sin (a1) * x + cos (a1) * y ;

根据角度转弧度公式：rad = deg * π / 180
texcoord 二维旋转代码

// 变量声明
float1 a1 = frac ( input_angle / 360 ) * 360 ;  // 角度     ( 使输入范围循环于 0-360 区间 )
float2 uv = input_uv ;                          // texcoord
float2 center = input_rotate_center ;           // 轴点

// 旋转
float deg = a1 * 3.1415926 / 180 ;              // 角度制 转 弧度制
float2 rotate_center = uv - center ;            // 修改旋转轴点
float x = cos(deg) * rotate_center.x - sin(deg) * rotate_center.y + center ;
float y = sin(deg) * rotate_center.x + cos(deg) * rotate_center.y + center ;
float2 texcoord_rotate = float2 (x,y) ;
 
return texcoord_rotate ;

```
