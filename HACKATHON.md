# 해커톤 2차 예선용 스킬 세트

## 설치 (Codex)
`h-*` 폴더를 `~/.agents/skills/` (사용자 전역) 또는 시험 프로젝트의 `.agents/skills/` 에 복사 → Codex 재시작.

```bash
git clone https://github.com/pbh7428-png/skills ~/skills-repo
mkdir -p ~/.agents/skills && cp -r ~/skills-repo/h-* ~/.agents/skills/
```

- `h-*` 스킬은 자동 호출을 꺼둠(`allow_implicit_invocation: false`). 기존 `dev-kickoff`·`artifact-review`와 설명이 겹쳐 엉뚱한 스킬이 잡히는 걸 막기 위함. **항상 `$h-스킬명`으로 직접 호출.**
- 시험 프로젝트 루트에 이 파일을 `AGENTS.md`로 복사해두면 스킬이 안 잡혀도 흐름이 항상 맥락에 들어감.

| 순서 | 스킬 | 언제 | 산출물 |
|---|---|---|---|
| 1-1 | `$h-readme-extract` | 시작 직후 (병렬) | `docs/01_requirements_table.md` |
| 1-3 | `$h-data-check` 1단계 | 시작 직후 (병렬) | 프로파일링 결과 |
| 1-4 | `$h-data-check` 2·3단계 | 추출표 완성 후 | `docs/02_data_check.md`, HR 질문 후보 |
| 2 | (HR 인터뷰 — 직접) | | `docs/interview.md` |
| 전 과정 | `$h-decision-log` | 결정할 때마다 / 마지막 서술형 | `docs/decision_log.md` |
| 3 | `$h-prd-trd` | 인터뷰 후 | `docs/PRD.md`, `docs/TRD.md` |
| 3 | `$h-gap-review` | PRD/TRD 직후 1회, 별도 에이전트 | 누락·위험 표 |

## 타임라인 (3.5시간 기준)
| 시간 | 단계 |
|---|---|
| 0:00–0:10 | h-readme-extract + 직접 정독 + h-data-check 1단계 (병렬) |
| 0:10–0:15 | h-data-check 2·3단계 |
| 0:15–0:35 | HR 인터뷰 → interview.md, KPI 우선순위, h-decision-log 시작 |
| 0:35–0:55 | h-prd-trd → h-gap-review 1회 |
| 0:55–1:00 | 테스트셋: 정상 샘플 + 엣지셋 |
| 1:00–1:45 | **MVP end-to-end** → 테스트 → **중간 제출** → 대규모 1회 시험 |
| 1:45–2:40 | 개선(병렬) + 수용 기준 테스트 + baseline 대비 KPI |
| 2:40–3:00 | 직접 실행 확인, 대규모 최종 검증, UI 정리 |
| 3:00–3:30 | **h-decision-log 서술형 모드** → 최종 제출 |

MVP 체크포인트와 서술형 시간은 절대 줄이지 말 것.

## HR 인터뷰 체크 (직접 진행)
- 산출물 범위, UI 필요 여부
- 절대 어기면 안 되는 조건
- KPI 우선순위
- 현재 불만/이번 개선의 이유 → "성공 기준에 포함되나요, 참고인가요?"
- 엣지 케이스 동작 (고장, 급증, 0)
- "이게 안 되면 결과를 못 쓰는 건 뭔가요?"
- h-data-check의 숫자 포함 질문 + 검증불가 조건 ①②

## 구현 지시 (MVP)
> TRD의 MVP 단계만 구현. 모든 모듈 입력→출력 끝까지 연결. 샘플 데이터 실행 + 핵심 수용 기준 통과가 완료 기준. 최적화·리팩터링 금지.

## 개선 지시
> {모듈}을 mvp→improved로 교체. 인터페이스 유지, 기존 테스트 전부 통과, baseline 대비 KPI 출력.
