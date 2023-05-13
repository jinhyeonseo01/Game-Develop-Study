# CPU 아키텍쳐

태그: CPU 아키텍처 종류에 관한 설명

# **대표적인 CPU 제조사**

## Intel

- x86 아키텍쳐의 CPU를 만듭니다.

## AMD

- Intel의 x86 호환 CPU를 만듭니다.

## ARM

- x86과 전혀 다른 아키텍쳐를 사용합니다.
- ARM이라는 회사가 존재하지만, 누구든지 ARM 기반으로 커스텀한 칩을 만들어 판매할 수 있습니다.
- 즉 M1칩은 ARM에서 제작된 것이 아닌, Apple에서 만든 ARM 호환 CPU입니다.

---

# **아키텍처 종류**

## x86 (32bit)

- Intel 기반 32bit CPU 입니다.
- 현존하는 PC 프로그램 대부분이 이 아키텍쳐를 지원합니다.
- Windows, Linux, Mac OS (BigSur 까지)

## x86_64, amd64 (64bit)

- Intel 기반 64bit CPU입니다.
- x86과 호환됩니다.
- AMD가 제작했으나, Intel과 크로스 라이센싱하여 둘다 사용하고 있습니다.
- Windows, Linux, Mac OS (BigSur 까지)

## arm (32bit)

- arm 기반 32bit CPU 입니다.
- x86과 호환되지 않습니다.
- Linux, Mac OS (Monterey 부터), Android, iOS, 공유기 등..

## arm64, arm64/v8 (64bit)

- arm 기반 64bit CPU 입니다.
- arm과 호환됩니다.
- Linux, Mac OS (Monterey 부터), Android, iOS, 공유기 등..

<aside>
💡 Windows도 ARM 버전을 개발 중이고 베타도 존재합니다만… 아직은 없습니다.

</aside>

---