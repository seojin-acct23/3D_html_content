[README.md](https://github.com/user-attachments/files/34724023/README.md)
# 3D 디지털 트윈 실습 안내

Three.js로 만든 두 개의 웹 실습 파일에 대한 실행 방법과 코드 구조 설명서입니다.

| 실습 | 파일 | 내용 |
|---|---|---|
| 스마트 교실 실습 | `smart_classroom_neon.html` | 교실 환경(온도·CO₂·조도)을 가상 센서로 시뮬레이션하고 설비를 조절 |
| 버스 공장 실습 | `bus_factory_digital_twin.html` | 전기 저상버스의 8단계 조립 공정을 3D로 재생하고 부품을 조회 |

두 파일 모두 **HTML 한 개로 완결**됩니다. CSS와 JavaScript가 파일 안에 들어 있고, 외부 이미지나 3D 모델 파일은 쓰지 않습니다. 화면에 보이는 모든 수치는 실제 센서·설비와 연결되지 않은 시뮬레이션 값입니다.

---

## 1. 실행 방법

### 1-1. 준비물

- **최신 브라우저**: Chrome 또는 Edge 권장 (WebGL과 ES 모듈, importmap을 지원해야 함)
- **인터넷 연결**: Three.js 라이브러리를 CDN(`cdn.jsdelivr.net`)에서 내려받으므로 오프라인에서는 3D 화면이 뜨지 않습니다.
- 별도 설치, 빌드, 로그인은 필요 없습니다.

### 1-2. 실행하는 세 가지 방법

**방법 A — 파일 더블클릭**

HTML 파일을 더블클릭해 브라우저로 엽니다. 가장 간단한 방법입니다.

**방법 B — 로컬 서버**

더블클릭으로 열리지 않거나 학교·회사 보안 정책으로 막힐 때 사용합니다. 파일이 있는 폴더에서 터미널을 열고 다음을 실행합니다.

```bash
python -m http.server 8000
```

그다음 브라우저 주소창에 `http://localhost:8000/index.html`을 입력합니다. VS Code의 Live Server 확장을 써도 됩니다.

**방법 C — GitHub Pages**

1. 저장소에 `index.html`, `smart_classroom_neon.html`, `bus_factory_digital_twin.html`을 **같은 폴더**에 올립니다.
2. 저장소 Settings → Pages에서 배포 브랜치를 지정합니다.
3. 발급된 주소로 접속하면 `index.html`의 카드에서 두 실습으로 이동합니다.

파일명이 `index.html`의 링크와 한 글자라도 다르면 404가 납니다(대소문자 포함).

### 1-3. 화면이 안 뜰 때

| 증상 | 원인과 조치 |
|---|---|
| 로딩 문구에서 멈춤 / "실행에 실패했습니다" | CDN 접속 실패. 인터넷 연결과 방화벽을 확인 후 새로고침 |
| 검은 화면만 보임 | 브라우저의 하드웨어 가속(WebGL)이 꺼져 있음. 설정에서 켜기 |
| 화면이 끊김 | 다른 탭을 닫거나 창 크기를 줄이기 |
| "그래픽 연결이 끊겼습니다" (교실) | GPU 연결이 일시적으로 끊긴 상태. 자동 복구되지 않으면 "다시 실행" 클릭 |

교실 파일은 실패 시 즉시(늦어도 14초 안에), 공장 파일은 10초 뒤에 안내 문구를 띄웁니다.

---

## 2. 조작 방법

### 공통 (3D 화면)

- 마우스 왼쪽 드래그: 회전
- 휠: 확대/축소
- 오른쪽 드래그: 이동
- 화면 폭이 900px 이하이면 좌우 패널이 숨고, 하단 메뉴 버튼으로 엽니다.

### 스마트 교실 실습

| 위치 | 기능 |
|---|---|
| 왼쪽 패널 | 시나리오 4종(수업 중·쉬는 시간·집중 환기·야간 소등), 일시정지, 권장 설정 적용 |
| 왼쪽 패널 슬라이더 | 재실 인원, 외부 자연광, 목표 온도, 환기 장치, LED 조명, 블라인드 개방 |
| 왼쪽 패널 하단 | 센서 라벨/학생 모델 표시 전환, 장면 JSON·센서 CSV·화면 PNG 내보내기 |
| 가운데 하단 | 카메라 시점 5종(교실 전체·학생 시점·전자칠판·창가·평면 조망)과 초기화 |
| 오른쪽 패널 | 온도·CO₂·조도·재실·소비 전력·경과 시간, CO₂ 추이 그래프, 이벤트 로그 |

기준을 벗어나면 해당 카드와 상단 상태창이 주황색으로 바뀝니다. 기준은 온도 20~27°C, CO₂ 1,000ppm 미만, 조도 300~700lux입니다.

### 버스 공장 실습

| 위치 | 기능 |
|---|---|
| 왼쪽 패널 | 공정 8단계 선택, 이전/재생/다음, 재생 속도(0.5~2.5배) |
| 왼쪽 패널 하단 | 분해 보기, X-RAY(외피 반투명), 자동 회전, 초기화 |
| 가운데 하단 | 카메라 시점 8종(전경·측면·전면·후면·상부·하부·실내·현재 공정) |
| 3D 화면 클릭 | 부품 선택 → 오른쪽 인스펙터에 이름·설명·가상 사양 표시 |
| 오른쪽 패널 | 진행률 링, 가상 KPI 6종, OEE 추이, 부품 인스펙터, 이벤트 로그 |

키보드 단축키: `Space` 재생/정지, `←` `→` 공정 이동, `Esc` 선택 해제.

---

## 3. 두 파일의 공통 문법 구조

두 파일은 같은 뼈대를 씁니다.

```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta ...>                         <!-- 문자 인코딩, 화면 폭, 테마 색 -->
  <style> ... </style>               <!-- ① 디자인(CSS) -->
</head>
<body>
  <div id="app"> ... </div>          <!-- ② 화면 구성(HTML) -->
  <script type="importmap"> ... </script>   <!-- ③ 라이브러리 주소 지정 -->
  <script type="module"> ... </script>      <!-- ④ 3D와 동작(JavaScript) -->
</body>
</html>
```

### ① CSS — 디자인

- **디자인 토큰**: `:root`에 색과 글꼴을 변수로 한 번 정의하고 `var(--mint)`처럼 재사용합니다. 색을 바꾸려면 이 블록만 고치면 됩니다.

  ```css
  :root{
    --bg:#050a12; --panel:#08121d; --line:#153049;
    --text:#d9ecff; --muted:#6f8ba8;
    --blue:#2f9bff; --mint:#2ff5c8; --warn:#ffb84d;
  }
  ```

- **3열 그리드**: `#app{display:grid;grid-template-columns:290px minmax(0,1fr) 310px}`로 [왼쪽 패널 | 3D 뷰어 | 오른쪽 패널]을 나눕니다.
- **플로팅 HUD**: 3D 화면 위의 상태창과 시점 버튼은 `position:absolute`로 띄우고 `backdrop-filter:blur()`로 반투명 유리 효과를 냅니다.
- **반응형**: `@media(max-width:900px)`에서 좌우 패널을 화면 밖으로 밀어 두었다가 `.open` 클래스가 붙으면 `transform`으로 끌어옵니다.

### ② HTML — 화면 구성

- `<aside>` 두 개(좌우 패널)와 `<main id="viewer">`(3D 영역)로 이루어집니다.
- 3D 캔버스는 HTML에 없습니다. JavaScript가 만들어 빈 `<div>`(교실 `#stage`, 공장 `#canvas-host`)에 넣습니다.
- 값이 바뀌는 요소에는 `id`를 붙여 JavaScript가 찾아 갱신합니다. 버튼 묶음은 `data-view="overview"` 같은 `data-*` 속성으로 구분합니다.

### ③ importmap — 라이브러리 불러오기

```html
<script type="importmap">
{"imports":{
  "three":"https://cdn.jsdelivr.net/npm/three@0.164.1/build/three.module.js",
  "three/addons/":"https://cdn.jsdelivr.net/npm/three@0.164.1/examples/jsm/"
}}
</script>
```

`three`라는 짧은 이름을 실제 CDN 주소에 연결합니다. 그래서 모듈 스크립트에서 아래처럼 쓸 수 있습니다.

```js
import * as THREE from 'three';
import { OrbitControls } from 'three/addons/controls/OrbitControls.js';
```

교실은 Three.js `0.164.1`, 공장은 `0.187.0`을 씁니다. 버전을 바꾸려면 importmap의 숫자 두 곳을 함께 고칩니다.

### ④ JavaScript — Three.js 기본 흐름

두 파일 모두 다음 순서를 따릅니다.

| 단계 | 하는 일 | 핵심 코드 |
|---|---|---|
| 1 | 렌더러 생성 | `new THREE.WebGLRenderer({antialias:true})` |
| 2 | 장면과 카메라 | `new THREE.Scene()`, `new THREE.PerspectiveCamera(42, 비율, near, far)` |
| 3 | 마우스 조작 | `new OrbitControls(camera, renderer.domElement)` |
| 4 | 조명 | `HemisphereLight`(환경광), `DirectionalLight`(그림자 주광), `PointLight`(네온) |
| 5 | 재질 | `MeshStandardMaterial({color, roughness, metalness})`를 미리 만들어 공유 |
| 6 | 물체 조립 | 상자·원기둥·구를 만드는 도우미 함수로 `Group`에 쌓기 |
| 7 | 상태와 UI | 상태 객체 하나에 값을 모으고, 이벤트가 오면 상태 → 화면 순으로 갱신 |
| 8 | 반복 렌더 | 매 프레임 애니메이션 계산 후 `renderer.render(scene, camera)` |

자주 쓰인 문법은 다음과 같습니다.

- **화살표 함수와 짧은 도우미**: `const $ = id => document.getElementById(id);`
- **구조 분해와 전개**: `for (const [w, d, x, z] of [...])`, `camera.position.set(...좌표배열)`
- **템플릿 문자열**: `` `Student_Desk_${번호}` ``
- **이중 반복문으로 배치**: 책상 6열×4행, 공장 기둥 등
- **`CanvasTexture`**: 2D 캔버스에 글자를 그려 3D 표면(전자칠판, 라벨, 간판)에 붙임
- **프레임률과 무관한 보간**: `1 - Math.exp(-dt * 계수)`로 부드럽게 목표값에 접근

---

## 4. 스마트 교실 실습 — 코드 구조

`<script>`가 세 개입니다.

| 순서 | 종류 | 역할 |
|---|---|---|
| 1 | `type="application/json" id="sceneSpec"` | 교실 치수, 가구 좌표, 초기값, 카메라 시점을 담은 설정 데이터 |
| 2 | 일반 스크립트 | 3D 시작 실패 시 안내 화면 표시(오류 감지, 14초 제한) |
| 3 | `type="module"` | 3D 장면과 시뮬레이션 본체 |

모듈 스크립트는 위에서 아래로 다음 순서입니다.

1. **설정 읽기**: `const SPEC = JSON.parse(...)`. 책상 좌표나 카메라 위치는 코드가 아니라 이 JSON에서 가져옵니다.
2. **렌더러·카메라·컨트롤**: 그림자는 `shadowMap.autoUpdate=false`로 한 번만 계산해 고정합니다. `clampTarget()`이 카메라 중심점을 교실 주변으로 제한합니다.
3. **도우미 함수**: `bx`(상자), `cyl`(원기둥), `sphere`(구), `rod`(두 점을 잇는 막대), `plane`, `group`, `texCanvas`(절차적 텍스처), `rng`(고정 난수).
4. **재질 묶음 `M`**: 벽, 바닥, 나무, 유리, 네온 등. 바닥과 벽 무늬는 캔버스로 직접 그려 만듭니다.
5. **장면 조립** (그룹 단위):
   - `School_Architecture`: 바닥, 앞벽, 낮은 절개벽, 기둥과 보
   - `Window_System`: 창 4칸과 블라인드
   - `Outdoor_Scenery`: 네온 격자 바닥, 건물, 나무
   - `Student_Desks_24` / `Seated_Students_24`: 책상·의자·학생 24세트
   - `Teacher_Zone`, `Smart_Board`, `HVAC_System`, `IoT_Sensors`, `Ceiling_Light_System`, `Digital_Twin_Overlays`(센서 라벨)
6. **벽 자동 절개 `updateWallCutaway()`**: 카메라가 앞벽이나 창가 벽 바깥으로 나가면 해당 벽을 숨깁니다. 경계에서 깜빡이지 않도록 숨김/복귀 기준을 다르게 둡니다.
7. **상태 객체 `sim`**: 재실 인원, 자연광, 목표 온도, 환기, LED, 블라인드와 계산 결과(온도, CO₂, 조도, 전력)를 보관합니다.
8. **갱신 함수**:
   - `readInputs()`: 슬라이더 값 → `sim`
   - `updateVisual()`: `sim` → 3D(조명 밝기, 블라인드 길이, 학생 수, 배경색)
   - `updateUI()`: `sim` → 숫자 카드, 경고 상태, 라벨, 전자칠판, 로그
   - `drawHistory()`: CO₂ 그래프
9. **이벤트 연결**: 시나리오, 권장 설정, 일시정지, 표시 전환, 카메라 시점, 내보내기, 서랍 메뉴.
10. **`animate()` 루프**: 가상 시간 진행(실제 1초 ≈ 가상 12초) → CO₂·온도 계산 → 공기 흐름 애니메이션 → 카메라 이동 → 렌더.
11. **안전장치**: 창 크기 변경 대응, WebGL 연결 끊김/복구 처리.

시뮬레이션 계산식(학습용 근사):

```text
CO₂ 목표값  = 430 + 인원 × 60 ÷ (0.8 + 환기% ÷ 50)
조도(lux)   = 자연광% × 3.8 × (0.35 + 0.65 × 블라인드% ÷ 100) + LED% × 3.5
온도 목표값 = 설정온도 + 인원 × 0.025 + 일사계수 × 0.60 − 환기% × 0.003
```

CO₂와 온도는 목표값으로 바로 바뀌지 않고 `현재값 += (목표 − 현재값) × (1 − e^(−dt/시간상수))`로 서서히 따라갑니다.

---

## 5. 버스 공장 실습 — 코드 구조

모듈 스크립트가 주석으로 A~R 구역으로 나뉘어 있어 찾기 쉽습니다.

| 구역 | 내용 |
|---|---|
| A | 공통 도우미(`$`, `pad2`, `V`) |
| B | 공정 데이터 `STAGES` — 8단계의 제목, 설명, 카메라 위치 |
| C | 렌더러, 장면, 카메라, OrbitControls |
| D | 조명(환경광, 그림자 주광, 네온 포인트 2개) |
| E | 공용 재질 `M`과 X-RAY 대상 재질 목록 |
| F | 도우미 `box`, `cyl`, `label`(글자 간판) |
| G | 공장 환경 — 격자 바닥, 컨베이어, 기둥·트러스, 스캔 게이트, 무인 운반차, 부유 입자 |
| H | 로봇 팔 4대 — `Group`을 겹쳐 관절 구조로 구성 |
| I | 버스 부품 34개 — `part(정의, 조립함수)`로 등록 |
| J | 상태 `state`와 조립 로직(`setStage`, `setAuto`, `setExplode`, `setXray`) |
| K | 카메라 시점 `VIEWS`와 이동 함수 `flyTo` |
| L | 부품 선택(Raycaster), 발광 테두리, 마우스 올림 툴팁 |
| M | 화면 갱신 — 공정 버튼, 상태창, 진행률, 인스펙터 |
| N | 버튼·키보드·서랍 메뉴 이벤트 |
| O | 가상 KPI(1초마다 무작위 변동)와 OEE 추이선 |
| P | 캔버스 크기 맞춤(`ResizeObserver`) |
| Q | 렌더 루프 `animate` |
| R | 초기화 — 1단계부터 자동 재생 시작 |

핵심 개념 세 가지:

**부품 등록 `part()`**

```js
part({ id:'roof', name:'루프 패널 · 공조 유닛', stage:4,
       desc:'...', spec:['알루미늄 / FRP','205 kg','1 식','접착 + 볼트'],
       scatter:[0,9,0], explode:[0,6.2,0] }, g => {
  box(g, 10.63, 0.2, 2.53, M.roof, 0, 3.47, 0);
  // ...
});
```

- `stage`: 몇 번째 공정에서 등장하는지(0부터)
- `scatter`: 조립 전 흩어져 있는 위치
- `explode`: 분해 보기일 때 벌어지는 위치
- 두 번째 인자(함수): 그 부품의 실제 형상을 만드는 코드

**조립 애니메이션**

`setStage(n)`이 `n`단계 이하의 부품을 활성화하면, 렌더 루프가 매 프레임 각 부품을 목표 위치(조립 위치·분해 위치·흩어진 위치 중 하나)로 `lerp`시킵니다. 같은 공정의 부품은 `delay`로 시차를 두고 차례로 들어옵니다.

**부품 선택**

클릭 좌표를 `Raycaster`로 3D 광선으로 바꿔 맞은 메시를 찾고, `userData.part`로 어느 부품인지 알아냅니다. 선택된 부품은 발광 복제 재질과 `EdgesGeometry` 외곽선으로 강조합니다. X-RAY 중에는 반투명 외피를 건너뛰고 안쪽 부품을 먼저 고릅니다.

성능을 위한 처리도 들어 있습니다. 롤러 88개는 `InstancedMesh`로, 입자 360개는 `Points`로 각각 한 번에 그립니다.

---

## 6. 두 파일 비교

| 항목 | 스마트 교실 | 버스 공장 |
|---|---|---|
| Three.js 버전 | 0.164.1 | 0.187.0 |
| 주제 | 환경 시뮬레이션(연속 값) | 조립 공정(단계 진행) |
| 설정 데이터 | 별도 JSON 블록(`sceneSpec`) | 코드 안 배열(`STAGES`, `VIEWS`) |
| 상태 객체 | `sim` | `state` |
| 사용자 입력 | 슬라이더 6개, 시나리오 | 공정 버튼, 재생, 부품 클릭 |
| 3D 물체 선택 | 없음 | Raycaster로 부품 선택 |
| 렌더 루프 | `requestAnimationFrame` | `renderer.setAnimationLoop` |
| 그림자 | 한 번 계산 후 고정 | 매 프레임 갱신 |
| 내보내기 | JSON, CSV, PNG | 없음 |
| 코드 작성 방식 | 한 줄에 여러 문장을 압축 | 구역 주석(A~R)과 줄 나눔 |

---

## 7. 직접 고쳐 보기

| 하고 싶은 것 | 고칠 곳 |
|---|---|
| 전체 색 바꾸기 | 두 파일의 `:root{ ... }` 색 변수 |
| 교실 초기값·시나리오 바꾸기 | `sceneSpec`의 `initialConditions`, 모듈 안 `cases` 객체 |
| 교실 경고 기준 바꾸기 | `updateUI()`의 `tw`, `co`, `lx` 조건식 |
| 교실 카메라 시점 추가 | `sceneSpec`의 `cameraViews`에 항목 추가 + 버튼에 `data-view` 지정 |
| 공장 공정 설명 바꾸기 | B 구역 `STAGES` 배열 |
| 공장 부품 추가 | I 구역에 `part({...}, g => {...})` 추가 |
| 버스 도장 색 바꾸기 | E 구역 `M.paint`의 `color` |
| 재생 속도 범위 바꾸기 | `<input id="speed">`의 `min`, `max` |

수정 후에는 브라우저에서 새로고침(`Ctrl+Shift+R`)하고, 화면이 뜨지 않으면 `F12` → Console 탭에서 오류 메시지를 확인합니다.
