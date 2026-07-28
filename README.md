# 스틱 플렉스 계산기

아이스하키 스틱의 플렉스를 몸무게와 **스틱 길이**로 함께 계산합니다.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Dependencies](https://img.shields.io/badge/dependencies-none-brightgreen.svg)
![Single file](https://img.shields.io/badge/build-not%20required-lightgrey.svg)

**→ [계산기 열기](https://chungchung234.github.io/hockey-flex/)**

---

## 소개

하키 스틱을 고를 때 가장 널리 쓰이는 기준은 `플렉스 = 몸무게 ÷ 2`입니다. 간단하지만 **스틱 길이를 전혀 반영하지 않는다는 문제**가 있습니다.

스틱이 얼마나 휘는지는 몸무게보다 길이에 훨씬 크게 좌우됩니다. 길이가 길면 지렛대가 길어져 같은 힘으로도 더 많이 휘고, 짧으면 그 반대입니다. 그래서 이 규칙은 키가 작거나 스틱을 짧게 쓰는 사람에게 필요 이상으로 뻣뻣한 스틱을 권하게 됩니다.

이 계산기는 길이를 정식 변수로 넣어 계산합니다.

```
flex = 몸무게(lbs) × 길이(in)² ÷ 7700 × 보정계수
```

의존성이 없는 단일 HTML 파일이며, 빌드 과정 없이 브라우저에서 바로 동작합니다.

## 주요 기능

- **단위 자동 환산** — kg·cm로 입력하고 lbs·in 값을 함께 확인
- **길이 입력 보조** — 정확한 길이를 몰라도 규격(시니어·인터·주니어·유스)과 잘라낸 길이로 계산하거나, 키로 추정
- **보정 프리셋** — 국내 동호회 · 해외 표준 · 파워슛/디펜스
- **결과 시각화** — 시판 규격 스냅, 탐색 범위, 몸무게÷2 대비 위치를 눈금자에 함께 표시
- **경량 체격 보정 안내** — 60kg 이하에서 계산값이 낮게 나오는 구간을 자동으로 알림
- **다크 모드 · 한국어/영어** — 첫 진입 시 기기 설정을 따르고, 이후 선택을 기억
- **모바일 우선** — 결과창 상단 고정, 스테퍼 입력

## 사용 방법

**1. 몸무게** — kg으로 입력합니다. lbs 환산값이 함께 표시됩니다.

**2. 스틱 길이** — 블레이드 힐(바닥이 샤프트 라인과 만나는 안쪽 지점)에서 샤프트 끝까지의 길이입니다. 블레이드 토 끝이 아닙니다.

정확한 값을 모른다면 두 가지 보조 수단이 있습니다.

- **규격에서 계산** — 구매한 규격을 선택하고 잘라낸 길이를 빼면 됩니다. 대부분 이 방법으로 해결됩니다.
- **키로 추정** — 키 × 0.87로 잡습니다. 스케이트를 신고 섰을 때 턱과 코 사이에 오는 대략적인 길이입니다.

**3. 보정 프리셋** — 기본값은 국내 동호회입니다. 해외 가이드가 슬랩샷 위주였던 시절을 기준으로 만들어져 국내 체감보다 뻣뻣하게 나오기 때문에, 원본 공식보다 약 13% 낮게 잡았습니다.

**결과 읽기** — 큰 숫자가 계산값이고, 아래 세 칸에 가장 가까운 시판 규격, 탐색 범위, 몸무게÷2 값이 나옵니다. 눈금자의 파란 띠가 탐색 범위, 빨간 눈금이 몸무게÷2 위치입니다.

## 계산 근거

스틱을 중앙에서 누르는 상황은 단순보 굽힘 문제이므로, 처짐 `d`는 다음과 같습니다.

```
d = F·L³ / (48·E·I)
```

플렉스 등급 `R`은 제조사가 약 1m의 고정 구간에서 측정하므로 `R = 48·E·I / L₀³`입니다. 두 식에서 `48EI`를 소거하고, 스틱이 길이에 비례하는 일정 비율만큼 휘도록 두면 다음이 남습니다.

```
R ∝ 몸무게 × 길이²
```

**길이가 제곱으로 들어가는 것이 핵심입니다.** 상수 7700은 62인치 스틱에서 결과가 "몸무게 ÷ 2"와 일치하도록 역산한 값입니다.

## 정확도와 한계

이 계산기가 내놓는 값은 근거의 강도가 항목마다 다릅니다.

| 항목 | 근거 |
|---|---|
| 플렉스 측정 방식 | **탄탄함** — `flex = 48EI/L³`, 단순보 굽힘 |
| `몸무게 × 길이²` 구조 | **탄탄함** — 같은 굽힘 이론에서 유도 |
| 상수 7700 | **경험칙** — 기존 통설에 맞춘 역산값이며 실측 피팅이 아님 |
| 보정계수 0.87 | **경험칙** — 국내 체감 기준, 검증되지 않음 |
| 체격 보정 지수 | **추정** — 문헌상 0.55~0.7 사이에서 갈림 |

### 자른 만큼 플렉스를 보정하지 마십시오

흔히 "1인치 자를 때마다 플렉스가 3~5 올라간다"고 하지만, 이는 업계 통설이지 측정값이 아닙니다.

플렉스는 지지점을 1m 간격으로 두고 가운데를 누르는 3점 굽힘으로 측정합니다. 지지점 바깥으로 나온 양 끝은 애초에 휘지 않으므로, 버트엔드를 잘라내도 측정되는 플렉스는 변하지 않습니다. 잘랐을 때 뻣뻣해지는 *느낌*의 실체는 손 간격이 좁아지는 것이며, 이는 자르든 자르지 않든 손을 모으면 동일하게 발생합니다.

이 계산기는 자른 뒤의 실제 길이를 이미 변수로 받으므로, 추가 보정은 이중 계산이 됩니다.

### 플렉스 숫자 하나가 감추는 것

표기 등급은 샤프트 중앙 1m 구간의 평균값입니다. 실측 자료에서는 83으로 표기된 스틱이 손잡이 쪽 74, 블레이드 쪽 99로 측정된 사례가 있습니다.

또한 실제 슛은 두 손이 지지점이 되고 힘은 블레이드 끝에 걸리는, 측정 조건과 전혀 다른 하중 상황입니다. 아래손 위치만으로도 체감 강성이 크게 달라집니다.

### 가벼운 체격에서는 계산값이 낮게 나옵니다

공식은 몸무게에 선형으로 비례하지만, 근력은 체중의 약 0.55~0.7승으로 증가합니다. 근력이 근단면적에 비례하고 체중은 부피에 비례하기 때문입니다. 따라서 70~80kg 부근에서 맞춰진 이 공식을 그보다 훨씬 가벼운 체격에 적용하면 실제로 낼 수 있는 힘을 과소평가합니다.

다만 이 지수는 체지방률과 성별에 따라 달라지므로 단일 값으로 확정할 수 없습니다. 계산기는 해당 구간에서 보정 범위를 안내만 하고, 최종 판단은 사용자에게 맡깁니다.

### 정리

몸무게 ÷ 2보다는 분명히 나은 출발점입니다. 다만 그 이상의 정밀도를 기대할 근거는 없으므로, 계산값 ±10% 범위에서 직접 쳐보고 결정하시기 바랍니다.

## 설정값 조정

주요 상수는 모두 `index.html` 안에 있습니다.

| 대상 | 위치 | 기본값 |
|---|---|---|
| 주 상수 | `render()` 함수 | 7700 |
| 보정 프리셋 | 스타일 버튼의 `data-mul` 속성 | 0.87 / 1.00 / 1.08 |
| 체격 보정 지수 | `render()` 함수 내 `Math.pow` | 0.30 / 0.45 (기준 80kg) |
| 탐색 범위 | `render()` 함수 | ±10% |
| 시판 규격 목록 | `RETAIL` 배열 | 20~110 |
| 규격별 길이 | `CATS` 배열 | cm |
| 키 → 길이 계수 | `hBtn` 핸들러 | 0.87 |

## 개선 방향

상수 7700과 보정계수 0.87은 모두 기존 통설에 맞춘 값이며 실측 데이터로 적합한 결과가 아닙니다. 정확도를 실질적으로 높이려면 회귀분석이 필요합니다.

```
ln(flex) = ln(a) + b·ln(몸무게) + c·ln(길이)
```

이때 `c = 2`는 굽힘 이론에서 나온 값이므로 고정할 수 있습니다. 미지수가 `a`와 `b` 둘뿐이므로 40~60명 규모의 표본으로도 추정이 가능합니다.

데이터를 모을 때 두 가지를 주의해야 합니다.

- **체중 분산이 확보되어야 합니다.** 표본이 특정 체중대에 몰려 있으면 `b`를 추정할 수 없습니다. 여성과 청소년 선수가 반드시 포함되어야 합니다.
- **만족도 응답에는 앵커링이 강하게 작용합니다.** 대부분 현재 쓰는 스틱을 긍정 평가하므로, "너무 뻣뻣 / 적절 / 너무 무름" 척도로 받아 순서형 회귀를 적용하거나 "적절" 응답만 필터링하는 편이 낫습니다.

관련 데이터나 개선 제안은 [이슈](https://github.com/chungchung234/hockey-flex/issues)로 남겨 주시면 반영을 검토하겠습니다.

## 배포

GitHub Pages로 호스팅할 수 있으며 터미널이 필요하지 않습니다.

1. 저장소 루트에 `index.html`을 둡니다.
2. `Settings` → `Pages` → Source를 `Deploy from a branch`로 설정합니다.
3. 브랜치는 `main`, 폴더는 `/ (root)`를 선택하고 저장합니다.

반영까지 최대 10분이 걸릴 수 있으며, 진행 상황은 `Actions` 탭에서 확인할 수 있습니다. 무료 플랜에서는 공개 저장소만 Pages를 지원합니다.

이후 `index.html`을 덮어쓰면 같은 주소로 갱신되므로 링크를 다시 배포할 필요가 없습니다.

로컬에서 확인하려면 `index.html`을 브라우저로 열면 됩니다. 별도의 서버가 필요하지 않습니다.

## 참고 자료

- **원 공식** — r/hockeyplayers, u/StickFlexScience, "Don't use half your body weight as your stick flex"
- **플렉스 측정 방식, 샤프트 구간별 편차, 릴리즈 타임 실측** — Rod Cross & Crawford Lindsey, *Flex of a Hockey Stick*, Tennis Warehouse University (2016)
- **하키 스틱 굽힘 물리** — D. Russell & R. Hunt, *The Physics Teacher*
- **근력의 체중 스케일링** — 기하학적 상사에 따른 2/3 지수 및 체지방률·성별에 따른 실측 편차 관련 문헌

## English

An ice hockey stick flex calculator based on **body weight and stick length**, rather than the common "half your body weight" rule — which ignores length entirely and significantly overestimates flex for shorter sticks.

```
flex = weight(lbs) × length(in)² ÷ 7700 × adjustment
```

Single HTML file, no dependencies, no build step. Includes dark mode and a Korean/English toggle, both following device settings on first load.

**On accuracy.** The beam-bending derivation (`W × L²`) is solid physics. The constant 7700 is not: it was reverse-fitted so the formula agrees with "half body weight" at 62 inches, and has never been validated against measured data. Treat the output as a starting point and test within ±10%.

**Do not add flex to compensate for cutting.** Flex is measured over a fixed 1 m span, and the sections beyond the supports do not bend at all — trimming the butt end leaves the rated flex unchanged. The stiffer *feel* comes from your hands moving closer together, which happens whether or not the stick is cut.

## 라이선스

[MIT](LICENSE)
