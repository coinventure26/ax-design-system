# Avatar — 컴포넌트 계약

- 아바타를 쓸 때는 이 문서의 variant, props, 금지 사항만 따른다. 문서에 없는 속성·variant·하위 컴포넌트는 만들지 않고 보고한다.
- 색·라운드는 `tokens.md`의 `mode` 변수만 쓴다. 컴포넌트 내부의 크기·간격·선 굵기는 아래 "내부 값"의 대응표를 따른다.
- 코드는 shadcn/ui `avatar`를 기준으로 한다.

## Purpose
- 사용자를 나타내는 원형 이미지다. 사용자 한 명은 `Avatar`, 여러 명을 겹쳐 보여줄 때는 `AvatarGroup`을 쓴다.
- 그룹에서 다 보여주지 못하는 인원 수는 `AvatarGroupCount`(`+3`)로 나타낸다.

## 구성
| Figma 컴포넌트 | 코드 | 역할 |
|---|---|---|
| `Avatar` | `Avatar` + `AvatarImage` | 이미지 아바타 한 개 |
| `AvatarGroup` | `AvatarGroup` | 아바타를 겹쳐 놓는 묶음 |
| `AvatarGroupCount` | `AvatarGroupCount` | 그룹 끝의 `+N` 원 |

## Variants
| 컴포넌트 | 속성 | 값 |
|---|---|---|
| `Avatar` | `Size` | `sm` / `default` / `lg` (기본값 `default`) |
| `AvatarGroupCount` | `Size` | `default` 하나뿐 (기본값 `default`) |
| `AvatarGroup` | `Count` (불리언) | `true` / `false` (기본값 `true`) |
| `AvatarGroup` | `Dir` | `LTR` 하나뿐. 코드 prop 없음, 항상 LTR이라 지정하지 않는다. |

## States
- 상태 변화(hover, focus, disabled 등)가 없다. 눌러서 동작하는 컴포넌트가 아니다.
- 아바타를 버튼 등의 안에 넣을 때 포커스 링 등 상태는 감싸는 컴포넌트의 규칙을 따른다.

## Behavior
- 항상 원형이다. 모서리는 `radius-full`이다.
- 이미지는 아바타 영역을 가득 채운다.
- 그룹은 왼쪽에서 오른쪽으로 8px씩 겹치고, 오른쪽 아바타가 위에 놓인다.
- 그룹 안 모든 항목(이미지 아바타와 `+N`)에 흰색 2px 링이 있어 겹친 경계를 구분한다.
- `+N` 원의 배경은 `muted`, 글자색은 `muted-foreground`다. N은 그룹에서 보이지 않는 인원 수다.
- 그룹은 `default` 크기만 쓴다. 그룹 안 아바타와 `+N`도 모두 `default`다.
- 그룹은 아바타 3개를 보여주고, 전체 인원이 4명 이상이면 `+N`(N = 전체 − 3)을 붙인다. 3명 이하이면 `+N`을 넣지 않는다.

## Props 대응표

### Avatar
| Figma | 코드 prop | 값 | 비고 |
|---|---|---|---|
| `Size` | `size` | `"sm"` / `"default"` / `"lg"` | 기본값 `"default"` (shadcn 기본값과 같다) |
| `Avatar image` 레이어 | `AvatarImage`의 `src`, `alt` | 문자열 | `alt`는 항상 적는다. Figma에는 없는 속성이다. |

### AvatarGroup
| Figma | 코드 | 값 | 비고 |
|---|---|---|---|
| `Count` | `AvatarGroupCount`를 자식으로 넣을지 여부 | `true` = 넣는다 / `false` = 넣지 않는다 | 전체 4명 이상이면 `true`, 3명 이하이면 `false` |
| `Dir` | 없음 | `LTR` 고정 | 지정하지 않는다. |
| (아바타 자리) | `Avatar` 3개 | | 그룹 안 `Avatar`는 모두 `size="default"`다. |

### AvatarGroupCount
| Figma | 코드 | 값 | 비고 |
|---|---|---|---|
| `Size` | 없음 (자체 `size` prop 없음) | | 그룹에서는 `default`만 쓴다. |
| 글자 `+3` | 자식 텍스트 | `"+N"` | N은 숫자 |

## 내부 값 (크기·간격·선)
Figma 변수에 웹 code syntax가 비어 있어서, 이 표가 Figma 값과 코드 값의 기준이다.

| 용도 | Figma 변수 | 값 | 코드 |
|---|---|---|---|
| `sm` 크기 | `w-6`, `h-6` | 24px | `size-6` |
| `default` 크기 | `w-8`, `h-8` | 32px | `size-8` |
| `lg` 크기 | `w-10`, `h-10` | 40px | `size-10` |
| 그룹 겹침 | `-space-x-2` | -8px | `-space-x-2` |
| 그룹 링 두께 | `border-2` | 2px, 바깥쪽 | `ring-2` |
| 그룹 링 색 | `background` | | `ring-background` |
| `+N` 글자 (`sm`) | 텍스트 스타일 `caption` | 12px / 18px | `text-xs` |
| `+N` 글자 (`default`, `lg`) | 텍스트 스타일 `body` | 14px / 22px | `text-sm` |

## 사용 토큰 (`tokens.md`)
| 변수 | 용도 |
|---|---|
| `radius-full` | 모든 아바타와 `+N` 원의 모서리 |
| `muted` | `+N` 원 배경 |
| `muted-foreground` | `+N` 글자색 |
| `background` | 그룹 링 색 |

## Constraints (금지)
- `AvatarBadge`(상태 점 뱃지)를 쓰지 않는다. 뱃지는 Avatar에서 제거했다.
- `AvatarGroupCount` 안에 아이콘(`+` 등)을 넣지 않는다. `Icon` variant는 제거했다.
- RTL(`Dir=RTL`)은 만들지 않는다.
- `size`는 `sm` / `default` / `lg` 세 가지만 쓴다. 이 밖의 크기(예: 48px)는 만들지 않는다.
- 아바타 모서리를 `radius-full` 외의 값으로 바꾸지 않는다.
- 그룹의 링 색·두께, 겹침 간격을 바꾸지 않는다.
- `AvatarImage`의 `src`는 필수다. 이미지 없이 글자(이니셜)로 대신하는 아바타(fallback)는 만들지 않고 `AvatarFallback`도 쓰지 않는다. 필요한 화면이 생기면 보고한다.
- 그룹에서 `sm`, `lg` 크기를 쓰지 않는다. 그룹은 아바타를 3개까지만 보여주고, 그 이상은 `+N`으로 나타낸다.

## Related Resources
- Figma: https://www.figma.com/design/OXPqr6Zl0VaDq6lBp0Z5Z3/AX-design-system--%EB%B8%8C%EB%9E%9C%EC%B9%98-?node-id=8107-421
  - `Avatar` 세트 `8107:484`, `AvatarGroupCount` 세트 `8107:523`, `AvatarGroup` 세트 `8107:546`
- Tokens: `tokens.md`
- 코드 기준: shadcn/ui `avatar` (https://ui.shadcn.com/docs/components/avatar)
