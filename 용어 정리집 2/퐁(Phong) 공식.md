# 퐁(Phong) 공식

설명: 조명에 의한 스페큘러를 수학적으로 표현하는 공식 (V dot R)
태그: 반사 공식

![Phong.png](Phong.png)

조명에 의한 스페큘러 반사를 나타내는 하이라이트를 수학적으로 표현한 퐁 공식은 아래와 같습니다.

**‘조명 벡터(L)를 노말 방향(N)으로 반사하는 반사 벡터(R)와 시선 벡터(V)의 내적으로 스페큘러가 표현됩니다.’**

**R · V**가 기본적인 공식입니다.

다만, 이 공식을 계산하기 위해서는 반사 벡터(R)를 계산해야 합니다.

R 반사 벡터의 계산 공식은 **‘R = 2N(L** · **N) - L’** 인데, 현재는 내적이 그리 무거운 연산이 아니지만 예전에는 반사 벡터를 구하기 위한 연산에 부담이 있었습니다. (까마득한 옛날..)

그래서 James F. Blinn이 1977년 간략화된 공식을 만들었고, 이것이 [블린-퐁(Blinn-Phong) 공식](블린-퐁(Blinn-Phong)%20공식.md)입니다.