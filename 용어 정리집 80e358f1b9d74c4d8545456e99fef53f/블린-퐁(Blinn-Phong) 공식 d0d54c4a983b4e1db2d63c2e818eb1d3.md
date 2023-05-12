# 블린-퐁(Blinn-Phong) 공식

설명: 퐁 공식을 간략화한 공식 (N dot H, N: Normal Vector, H: Half Vector)
태그: 반사 공식

![Blinn-Phong.png](%E1%84%87%E1%85%B3%E1%86%AF%E1%84%85%E1%85%B5%E1%86%AB-%E1%84%91%E1%85%A9%E1%86%BC(Blinn-Phong)%20%E1%84%80%E1%85%A9%E1%86%BC%E1%84%89%E1%85%B5%E1%86%A8%20d0d54c4a983b4e1db2d63c2e818eb1d3/Blinn-Phong.png)

퐁 공식을 간략화한 블린-퐁 공식은 아래와 같습니다.

**‘조명 벡터(L)과 시선 벡터(V)의 중간 값인 ‘하프 벡터(V)’를 구하고, 이를 노말 벡터(N)과 내적한다’**

**H · N**이 기본적인 공식입니다. ****

결과는 그리 다르지 않지만, 스페큘러가 기울어져서 표면을 넘어갈 때 그 차이를 보입니다.

테스트 영상 보기 : [https://chulin28ho.tistory.com/708](https://chulin28ho.tistory.com/708)