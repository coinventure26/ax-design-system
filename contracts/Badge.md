# Badge — 컴포넌트 계약

- 배지를 쓸 때는 이 문서의 variant, props, 금지 사항만 따른다. 문서에 없는 속성·variant·색은 만들지 않고 보고한다.
- 색·라운드는 `tokens.md`의 `mode` 변수만 쓴다. 컴포넌트 내부의 크기·간격은 아래 "내부 값"의 대응표를 따른다.
- 코드는 shadcn/ui `badge`를 기준으로 한다. 단, `success` variant는 shadcn 기본 코드에 없어서 추가가 필요하다.

## Purpose
- 항목의 상태나 종류를 짧은 글자로 알려주는 작은 라벨이다. 누르는 버튼이 아니다.
- 예: 출석 상태(출석 / 지각 / 결석 / 예정), 글 분류(질문 / 공유 / 후기).

## 구성
| Figma 컴포넌트 | 코드 | 역할 |
|---|---|---|
| `Badge` | `Badge` | 글자 하나(선택으로 왼쪽 아이콘 하나)가 들어가는 배지 |

## Variants
| 속성 | 값 |
|---|---|
| `State` | `Default` / `Secondary` / `Destructive` / `Outline` / `Ghost` / `Success` (기본값 `Default`) |
| `Left icon` (불리언) | `true` / `false` (기본값 `false`) |

- 오른쪽 아이콘(`Right icon`)은 제거했다.
- 커스텀 컬러(파랑·하늘·보라 등)는 만들지 않는다. 초록은 `Success`, 빨강은 `Destructive`를 쓴다.

## 용도 기준 (어떤 state를 쓸까)
| 의미 | state | 화면 사례 |
|---|---|---|
| 성공·완료 | `Success` | 출석 |
| 위험·문제 | `Destructive` | 결석, 지각 |
| 일반 정보 | `Secondary` 또는 `Outline` | 예정, 질문, 공유, 후기 |
| 가장 눈에 띄어야 하는 표시 | `Default` | 화면에서 꼭 필요한 곳에서만 |
| 배경 없이 약하게 | `Ghost` | 다른 요소 옆에 붙는 보조 표시 |

## States
- 상태 변화(hover, focus, disabled 등)가 없다.
- 링크로 쓸 때(`asChild`)의 hover·포커스 링은 감싸는 요소(링크)의 규칙을 따른다.

## Behavior
- 항상 완전히 둥근 알약 모양이다. 모서리는 `radius-full`이다.
- 글자는 한 줄이고 줄바꿈하지 않는다. 가로는 글자 길이에 맞춰 늘어난다(hug).
- 아이콘은 글자 왼쪽에만 둔다. 아이콘과 글자 사이는 4px이다.
- `Outline`은 `border` 색의 1px 테두리가 있고 배경이 없다. `Ghost`는 배경과 테두리가 없다.
- 아이콘은 Lucide만 쓰고, 아이콘 종류는 `INSTANCE_SWAP`으로 바꾼다.

## Props 대응표
| Figma | 코드 prop | 값 | 비고 |
|---|---|---|---|
| `State` | `variant` | `"default"` / `"secondary"` / `"destructive"` / `"outline"` / `"ghost"` / `"success"` | 기본값 `"default"`. `"success"`는 shadcn 기본에 없어서 `badge.tsx`에 추가해야 한다. |
| `Left icon` | 아이콘 자식 | `true` = 아이콘을 자식으로 넣고 `data-icon="inline-start"`를 붙인다 / `false` = 넣지 않는다 | 스피너도 같은 방식이다. |
| 글자 | 자식 텍스트 | 문자열 | |
| (링크로 쓸 때) | `asChild` | | 링크 요소를 배지 모양으로 그릴 때 쓴다. Figma에는 없는 속성이다. |

### `success` variant 추가 시 클래스 기준
| state | 배경 | 글자 | 비고 |
|---|---|---|---|
| `Destructive` | `bg-destructive/10` | `text-destructive` | shadcn 기본 |
| `Success` | `bg-success/10` | `text-success` | 추가 필요. 개발 쪽 `globals.css`에 `--success`와 `@theme inline`의 `--color-success`가 있어야 한다. |

## 내부 값 (크기·간격·글자)
| 용도 | Figma 변수 | 값 | 코드 |
|---|---|---|---|
| 가로 여백 | `_px-2(미사용)` | 8px | `px-2` |
| 세로 여백 | `_py-0,5(미사용)` | 2px | `py-0.5` |
| 아이콘과 글자 간격 | `gap-1` | 4px | `gap-1` |
| 아이콘 크기 | (변수 없음) | 12px | `size-3` |
| 글자 | 텍스트 스타일 `caption-strong` | 12px / 18px, Medium | `text-xs font-medium` |
| 모서리 | `radius-full` | 9999px | `rounded-full` |

- 가로·세로 여백은 Figma에서 `_`로 시작하는 미사용 변수(`_px-2`, `_py-0,5`)에 연결되어 있다. 기준 변수가 정해질 때까지 위 표의 값(px)과 코드를 기준으로 한다.

## 사용 토큰 (`tokens.md`)
| state | 배경 | 글자·아이콘 | 테두리 |
|---|---|---|---|
| `Default` | `primary` | `primary-foreground` | 없음 |
| `Secondary` | `secondary` | `secondary-foreground` | 없음 |
| `Destructive` | `destructive-subtle` | `text-destructive` | 없음 |
| `Outline` | 없음 | `foreground` | `border` |
| `Ghost` | 없음 | `foreground` | 없음 |
| `Success` | `success-subtle` | `text-success` | 없음 |

## Constraints (금지)
- 오른쪽 아이콘(`Right icon`, `data-icon="inline-end"`)을 쓰지 않는다.
- RTL 배지를 만들지 않는다.
- `bg-green-50`, `dark:bg-green-800` 같은 색 클래스나 아토믹 색(`tw/colors`)을 덮어써서 커스텀 컬러를 만들지 않는다. 필요한 색은 위 6개 state 안에서 고른다.
- 위 6개 밖의 variant(예: 노랑·파랑 배지, 숫자 카운트 배지)를 임의로 만들지 않는다. 필요하면 보고한다.
- 글자를 두 줄로 쓰거나 배지 안에 글자 외 요소(버튼, 입력창 등)를 넣지 않는다.
- 아이콘은 하나까지만 넣고 Lucide가 아닌 아이콘 세트를 쓰지 않는다.
- 배지 모서리를 `radius-full` 외의 값으로 바꾸지 않는다.
- 상태를 색만으로 구분하지 않는다. 출석·지각·결석은 항상 글자를 같이 쓴다.

## Related Resources
- Figma: https://www.figma.com/design/OXPqr6Zl0VaDq6lBp0Z5Z3/AX-design-system--%EB%B8%8C%EB%9E%9C%EC%B9%98-?node-id=8110-4744
  - `Badge` 세트 `8110:4773`
- Tokens: `tokens.md`
- 코드 기준: shadcn/ui `badge` (https://ui.shadcn.com/docs/components/badge)
