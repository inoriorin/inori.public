```
// dissolve
float1 dissolve_base = saturate ( ( ( in_dissolve + 1 ) - ( in_dissolve_value * 2 ) ) * in_hardness ) ;
float1 dissolve_edge = saturate ( dissolve_base - saturate ( ( ( in_dissolve + 1 ) - ( in_dissolve_value * 2 + in_dissolve_edge ) ) * in_hardness ) ) * in_edge_int ;

edge = dissolve_dege ;
return dissolve_base ;
 
```
