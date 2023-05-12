# 레이 마칭 (Ray Marching)

1. 폴리곤이 아닌 다른 것을 렌더링하는 방법 → 볼륨으로 보이게됨
2. 최단거리만을 이용해서 렌더링을하는 기법임
3. 가장 가까운 표면까지의 거리 + 거리 + 거리 … 을 한 후 일정 거리 미만이거나 횟수로 제한을 둬서 해당 지점이 표면이라고 가정한다.

쓰면 뭐가 좋은지?

1. 모델 두개를 섞을때 폴리곤 기반이면 그냥 새로 만들어야하지만 레이 마칭은 그럴 필요가 없음
    1. 서로 뺀다던지 특이한 방식으로 합친다던지 가능함

그럼 레이 마칭만으로 렌더링 되나요??

1. 쉐이더 코드나 텍스쳐를 만들어야함
    1. 맥스나 마야같은 툴도 없어서 쌩임
2. 잘 못 만들면 (엄청) 무거워짐
3. 섞어쓰면 좋음!

지금 사용 중인 곳

1. 구름, 안개, 그림자 등 ← 이 부분이 짱이라함
2. 장난감, 테크 데모 ← 알고리즘 기반이라 폴리곤으로 표현하긴 어렵지만 도형 기반으론 쉬운걸 표현하기 좋음
3. Scene Depth를 통해 폴리곤 렌더링과 합치기 쉬움

만들어야할 것

1. 도형 별 거리 구하는 함수
    1. [https://iquilezles.org/articles/distfunctions2d/](https://iquilezles.org/articles/distfunctions2d/)
    2. [http://mercury.sexy/hg_sdf/](http://mercury.sexy/hg_sdf/)
2. 거리 함수
    1. Union : 합성, 더 가까운 곳을 구하면 됨
    2. Intersect : 교차, 더 먼 곳을 구하면 됨
    3. Subtract : 빼기

[Ray Marching Fog With Blue Noise](https://blog.demofox.org/2020/05/10/ray-marching-fog-with-blue-noise/)