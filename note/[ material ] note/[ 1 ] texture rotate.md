```
已知长度为 1 的向量 n = ( x , y ) ; n 以 ( 0 , 0 ) 为中心逆时针旋转 a1 度 得到 v ( x , y ) ; 推算 v ( x , y )
v.x = cos ( a1 + a2 ) = cos (a1) * cos (a2) - sin (a1) * sin (a2) = cos (a1) * x - sin (a1) * y ;
v.x = -sin ( a1 + a2 ) = -sin (a1) * -sin (a2) - cos (a1) * cos (a2) = -sin (a1) * x - cos (a1) * y ;
 
根据图例所示
向量长度为 1 时 ， n (x,y) 经过 a1 旋转后 得到 v (cos(a1),-sin(a1))

根据角度转弧度公式：deg = rad * 180 / π
texcoord 二维旋转代码

// 变量声明
float a1 = input_angle ;               // 角度
float2 uv = input_uv ;                 // texcoord
float2 center = input_rotate_center ;  // 轴点

// 旋转
float deg = a1 * 180 / 3.1415926 ;
float x = cos(a1) * uv.x - sin(a1) * uv.y ;
float y = -sin(a1) * uv.x - cos (a1) * uv.y;
 

```
![image](https://github.com/inoriorin/inori.public/blob/main/image/1/%5B%202%20%5D%20material/image_001.png)
