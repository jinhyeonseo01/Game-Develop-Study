# Sobel Outline

설명: Depth(뎁스) 기반 아웃 라인, Depth Normal을 둘다 쓰기도 한다.
태그: 아웃라인

이웃UV 와의 Normal, Depth의 차이를 이용한 Outline를 그리는 기술

Depth

```
float SobelSampleDepth(Texture2D t, SamplerState s, float2 uv, float3 offset)
{
    float pixelCenter = LinearEyeDepth(t.Sample(s, uv).r);
    float pixelLeft   = LinearEyeDepth(t.Sample(s, uv - offset.xz).r);
    float pixelRight  = LinearEyeDepth(t.Sample(s, uv + offset.xz).r);
    float pixelUp     = LinearEyeDepth(t.Sample(s, uv + offset.zy).r);
    float pixelDown   = LinearEyeDepth(t.Sample(s, uv - offset.zy).r);

    return SobelDepth(pixelCenter, pixelLeft, pixelRight, pixelUp, pixelDown);
}
```

Normal

```
float4 SobelSample(Texture2D t, SamplerState s, float2 uv, float3 offset)
{
    float4 pixelCenter = t.Sample(s, uv);
    float4 pixelLeft   = t.Sample(s, uv - offset.xz);
    float4 pixelRight  = t.Sample(s, uv + offset.xz);
    float4 pixelUp     = t.Sample(s, uv + offset.zy);
    float4 pixelDown   = t.Sample(s, uv - offset.zy);

    return abs(pixelLeft  - pixelCenter) +
           abs(pixelRight - pixelCenter) +
           abs(pixelUp    - pixelCenter) +
           abs(pixelDown  - pixelCenter);
}
```

```
float4 FragMain(VaryingsDefault i) : SV_Target
{
    float3 offset = float3((1.0 / _ScreenParams.x), (1.0 / _ScreenParams.y), 0.0) * _OutlineThickness;
    float3 sceneColor = SAMPLE_TEXTURE2D(_MainTex, sampler_MainTex, i.texcoord).rgb;

    // Sample the normal buffer and build a composite scalar value
    float3 sobelNormalVec = SobelSample(_CameraGBufferTexture2, sampler_CameraGBufferTexture2, i.texcoord.xy, offset).rgb;
    float sobelNormal = sobelNormalVec.x + sobelNormalVec.y + sobelNormalVec.z;

    // Modulate the outline color based on it's transparency
    float3 outlineColor = lerp(sceneColor, _OutlineColor.rgb, _OutlineColor.a);

    // Calculate the final scene color
    color = lerp(sceneColor, outlineColor, sobelNormal);
    return float4(color, 1.0);
}
```

`sobelNormal = pow(sobelNormal * _OutlineNormalMultiplier, _OutlineNormalBias);`

[https://www.vertexfragment.com/ramblings/unity-postprocessing-sobel-outline/](https://www.vertexfragment.com/ramblings/unity-postprocessing-sobel-outline/)

[https://www.youtube.com/watch?v=_KxiPQTvjLg&ab_channel=AETuts](https://www.youtube.com/watch?v=_KxiPQTvjLg&ab_channel=AETuts)