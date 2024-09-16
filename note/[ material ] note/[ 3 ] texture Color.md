```
// 变量声明
float3 color = in_color ;

//refine
float3 desaturated_color = float3 (0.3,0.59,0.11) ; // 定义去饱和颜色
float3 desaturation_color =lerp ( color , dot ( desaturated_color , color ) , in_desaturation) ; // 去饱和
float3 refine_color = lerp ( desaturation_color * in_base_int  , pow ( desaturation_color , in_power ) * in_height_int , in_refine_lerp ) ;

//lerp
float3 re_white_color = dot ( desaturated_color , refine_color) ;
 
float3 lerp_color = lerp ( refine_color , lerp( in_shadow_color , in_height_color , re_white_color.x ) , in_lerp_switch ) ; // 假开关

return lerp_color ;
 
``` 
