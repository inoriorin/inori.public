```
// 变量声明
float3 color = in_color ;

//refine
float3 desaturated_color = (0.3,0.59,0.11) ; // 定义去饱和颜色
float3 desaturation_color = ( 1 - in_desaturation ) * dot(color,desaturated_color) + in_desaturation * color ; // 去饱和
float3 refine_color = lerp ( pow ( desaturation_color , in_power ) * in_height_int , desaturation_color * in_base_int , in_refine_lerp ) ;

//lerp
float3 re_white_color = dot(refine_color,desaturated_color) * refine_color ;
 
float3 lerp_color = lerp ( refine_color , lerp( in_height_color , in_shadow_color , re_white_color.x ) , in_lerp_switch ) ; // 假开关

return lerp_color ;
 
``` 
