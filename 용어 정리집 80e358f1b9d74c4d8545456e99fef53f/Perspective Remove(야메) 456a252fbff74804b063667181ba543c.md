# Perspective Remove(야메)

설명: Nilo Shader의 작업물을 야메로 직접 실험한 추론한 내용.

View Space에서의 카메라 방향을 기준으로 Model의 Vertex를 Local Space에서 압축한 결과물일 것이라는 추론.

```
float4x4 viewMatrix = UNITY_MATRIX_P;
float aspect = (_ScreenParams.x/_ScreenParams.y);

float4 offset = mul(UNITY_MATRIX_MV, float4(0,1,0,1));
float4 positioonVS = mul(UNITY_MATRIX_MV, i.position);

positioonVS.z = lerp(positioonVS.z, offset.z + (positioonVS.z-offset.z)*_Fov, i.position.y);
o.position = mul(UNITY_MATRIX_P, positioonVS);
o.positionWS = float4(TransformObjectToWorld(i.position.xyz),1);
#if defined(_MAIN_LIGHT_SHADOWS_SCREEN) && !defined(_SURFACE_TYPE_TRANSPARENT)
    o.shadowCoord = ComputeScreenPos(o.position);
#endif
OUTPUT_LIGHTMAP_UV(i.staticLightmapUV, unity_LightmapST, o.staticLightmapUV);
o.uv0 = i.uv0.xy * _MainTex_ST.xy + _MainTex_ST.zw;
```

[https://drive.google.com/file/d/1jjJF3y6f25-HiAL7pJaW4h0g6oWE2DRi/view?usp=share_link](https://drive.google.com/file/d/1jjJF3y6f25-HiAL7pJaW4h0g6oWE2DRi/view?usp=share_link)

[https://drive.google.com/file/d/17xOKAvpivq2uK-hRA91xJA2txr_sIw4V/view?usp=share_link](https://drive.google.com/file/d/17xOKAvpivq2uK-hRA91xJA2txr_sIw4V/view?usp=share_link)