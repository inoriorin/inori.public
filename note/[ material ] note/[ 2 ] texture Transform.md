```
// 变量声明
float1 rotate = frac ( in_rotate / 360 ) * 360 ;  // 角度     ( 使输入范围循环于 0-360 区间 )
float2 uv = in_uv ;                          // texcoord
float2 center = in_rotate_center ;           // 轴点

// rotate
float deg = rotate * 3.1415926 / 180 ;              // 角度制 转 弧度制
float2 rotate_center = uv - center ;            // 修改旋转轴点
float1 cx = cos(deg) * rotate_center.x - sin(deg) * rotate_center.y + center ;
float1 cy = sin(deg) * rotate_center.x + cos(deg) * rotate_center.y + center ;
float2 texcoord_rotate = float2 (cx,cy) ;
 
// return texcoord_rotate ;
 
// 变量声明
float2 tiling = {(in_tiling_x * in_dynamic_tx),(in_tiling_y * in_dynamic_ty)}  ;
float2 scale = {(in_scale_x),(in_scale_y)} ;
float1 panner = in_panner + in_dynamic_p ;
float2 offset = {(in_offset_x),(in_offset_y)} ; // 用于修正部分 UV 溢出导致的问题

// transform
float2 texcoord_tiling = tiling * ( ( texcoord_rotate - in_rotate_center ) * scale + in_rotate_center ) ;

float2 offset_dir = { ( sin(frac(in_rotate) * 6.283 )) , ( cos(frac(in_rotate) * 6.283 )) } ;
 
float2 texcoord_offset = ( offset_dir * lerp(panner * in_time,panner, saturate ( in_panner_switch ) ) ) + offset + texcoord_tiling ; // 假开关 不产生分支消耗 但会增加无用节点

// saturate clamp
float2 texcoord_clamp = {(lerp(texcoord_offset.x,saturate(texcoord_offset.x),in_clamp_x)),(lerp(texcoord_offset.y,saturate(texcoord_offset.y),in_clamp_y))} ;
 
float2 texcoord_output = texcoord_clamp + in_noise ;
 
return texcoord_output ;
 
 
```

