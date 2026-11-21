# Tokens — `mode` 컬렉션 변수 (색·라운드)

- **화면**에서는 이 목록의 `mode` 변수만 사용한다. 목록에 없는 변수와 `tw/*`, `rdx/*`는 사용하지 않는다.
- **컴포넌트 내부**의 크기·간격·선 굵기는 이 문서가 아니라 `contracts/`의 해당 컴포넌트 문서(Figma↔코드 대응표)를 기준으로 한다. 대응표에 적힌 값은 `tw/*` 변수여도 위반이 아니다. 컴포넌트 안의 색과 라운드는 이 문서의 `mode` 변수를 쓴다.
- 색 값은 Figma의 `mode` 컬렉션(light mode)이 원본이다. 이 문서에는 색 값을 적지 않는다.
- 웹 코드는 `globals.css`의 CSS 변수 이름이다.

## 화면 기본
| 변수 | 용도 | 웹 코드 |
|---|---|---|
| `background` | 화면 전체 배경 | `var(--background)` |
| `foreground` | 기본 글자색 | `var(--foreground)` |
| `card` | 카드 배경 | `var(--card)` |
| `card-foreground` | 카드 위 글자색 | `var(--card-foreground)` |
| `popover` | 팝오버, 드롭다운, 다이얼로그 배경 | `var(--popover)` |
| `popover-foreground` | 팝오버 위 글자색 | `var(--popover-foreground)` |

## 강조·보조
| 변수 | 용도 | 웹 코드 |
|---|---|---|
| `primary` | 주요 버튼 등 가장 눈에 띄는 색 | `var(--primary)` |
| `primary-foreground` | `primary` 위 글자·아이콘 | `var(--primary-foreground)` |
| `secondary` | 보조 버튼 배경 | `var(--secondary)` |
| `secondary-foreground` | `secondary` 위 글자 | `var(--secondary-foreground)` |
| `accent` | hover, 선택된 항목 배경 | `var(--accent)` |
| `accent-foreground` | `accent` 위 글자 | `var(--accent-foreground)` |
| `muted` | 덜 중요한 영역 배경 | `var(--muted)` |
| `muted-foreground` | 보조 설명 글자 | `var(--muted-foreground)` |

## 경계·입력
| 변수 | 용도 | 웹 코드 |
|---|---|---|
| `border` | 구분선, 카드 테두리 | `var(--border)` |
| `input` | 입력창 테두리 | `var(--input)` |
| `ring` | 키보드 포커스 링 | `var(--ring)` |

## 위험(Destructive)
| 변수 | 용도 | 웹 코드 |
|---|---|---|
| `destructive` | 삭제·신고 등 위험 동작의 강한 색 | `var(--destructive)` |
| `destructive-subtle` | 위험 동작 버튼의 옅은 배경 | `color-mix(in oklab, var(--destructive) 10%, transparent)` |
| `text-destructive` | 위험을 나타내는 글자·아이콘 색 | `var(--destructive)` |

## 성공(Success)
| 변수 | 용도 | 웹 코드 |
|---|---|---|
| `success` | 성공·완료를 나타내는 강한 색 | `var(--success)` |
| `success-subtle` | 성공 상태 배지의 옅은 배경 | `color-mix(in oklab, var(--success) 10%, transparent)` |
| `text-success` | 성공을 나타내는 글자·아이콘 색 | `var(--success)` |

- shadcn 기본 `globals.css`에는 `--success`가 없다. 개발 쪽에서 `--success`와 `@theme inline`의 `--color-success`를 추가해야 한다.

## 특정 용도에서만
| 변수 | 용도 | 웹 코드 |
|---|---|---|
| `chart-1` ~ `chart-5` | 차트 계열 색. 차트에서만 사용 | `var(--chart-1)` ~ `var(--chart-5)` |
| `sidebar` | 사이드바 배경. 사이드바 안에서만 사용 | `var(--sidebar)` |
| `sidebar-foreground` | 사이드바 글자색 | `var(--sidebar-foreground)` |
| `sidebar-primary` | 사이드바 강조색 | `var(--sidebar-primary)` |
| `sidebar-primary-foreground` | `sidebar-primary` 위 글자 | `var(--sidebar-primary-foreground)` |
| `sidebar-accent` | 사이드바 hover, 선택 배경 | `var(--sidebar-accent)` |
| `sidebar-accent-foreground` | `sidebar-accent` 위 글자 | `var(--sidebar-accent-foreground)` |
| `sidebar-border` | 사이드바 테두리 | `var(--sidebar-border)` |


## 라운드
- 기본은 `radius-md`, 카드와 큰 영역은 `radius-lg`다.
- 웹 코드는 shadcn 기본 계산식(`--radius` 10px 기준)이다. 개발 쪽 `@theme inline`과 같은지 확인이 필요하다.

| 변수 | 값 | 용도 | 웹 코드 |
|---|---|---|---|
| `radius-none` | 0px | 배경, 페이지 전체 영역처럼 모서리가 없는 곳 | `0` |
| `radius-md` | 8px | 버튼, 입력창 등 기본 모서리 | `calc(var(--radius) - 2px)` |
| `radius-lg` | 10px | 카드와 큰 영역의 모서리 | `var(--radius)` |
| `radius-full` | 9999px | 아바타, 뱃지처럼 완전히 둥근 모서리 | `9999px` |

## 아직 정해지지 않은 항목
- `border-width`, `stroke-width`: 웹 코드 이름 확인 전이다.

## 사용 금지
- `_sidebar-ring(미사용)`, `_background-color(미사용)`, `_semantic-background(미사용)`, `_semantic-border(미사용)`, `_semantic-foreground(미사용)`
- `_radius-xs(미사용)`, `_radius-sm(미사용)`, `_radius-xl(미사용)`, `_radius-2xl(미사용)`, `_radius-3xl(미사용)`, `_radius-4xl(미사용)`
- `_dark (미사용)` 모드
