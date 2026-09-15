# wsidd · What should I did & do?

**프로젝트의 전체 작업 흐름과 현재 진행 상태를 근거에 따라 정리하는 Codex 스킬입니다.**

코드, 문서, Git 변경사항, 테스트 기록, 산출물을 확인해 완료·진행 중·미시작을 구분합니다. 근거가 부족한 항목은 확인 필요로 남깁니다. 프로젝트 상태를 검토하는 요청에는 읽기 중심으로 동작합니다.

## 사용 예시

프로젝트가 열린 Codex 작업에서 요청합니다.

```text
$wsidd 이 프로젝트의 전체 작업 흐름을 보여 줘.
완료, 진행 중, 아직 시작하지 않은 작업을 구분하고
각 상태의 근거와 다음에 해야 할 일을 정리해 줘.
```

```text
$wsidd 현재 코드와 테스트 기록을 기준으로 배포 준비 상태를 검토해 줘.
실제로 검증된 부분과 아직 확인이 필요한 부분을 구분해 줘.
```

## 결과 구성

- 전체 상태 한 문장과 확인 날짜
- 프로젝트에 맞는 순서로 정리한 작업 흐름
- 단계별 상태·근거·남은 조건을 담은 표
- `Now`: 현재 작업의 초점
- `Next`: 의존관계를 고려한 다음 행동 1~3개
- `Risks / unknowns`: 판단에 영향을 주는 미확인 사항

| 표시 | 상태 | 판단 기준 |
| --- | --- | --- |
| ✅ | Completed | 필요한 결과물과 충족 조건을 확인함 |
| 🟡 | In progress | 구체적인 작업은 시작했지만 남은 조건이 있음 |
| ⚪ | Not started | 계획·요구사항이 있으나 구현 근거를 찾지 못함 |
| ❓ | Needs confirmation | 근거가 부족하거나 서로 충돌함 |

코드의 존재만으로 실행 성공이나 현장 적용 완료를 주장하지 않습니다. 오래된 테스트 결과, 정적 검사, 모의 실험, 실제 운영 상태도 구분합니다. 자세한 판정 기준은 [evidence-rubric.md](skills/wsidd/references/evidence-rubric.md)에 있습니다.

## 설치 — Windows PowerShell

원하는 폴더에서 저장소를 받습니다.

```powershell
git clone https://github.com/shippre/wsidd.git
Set-Location -LiteralPath .\wsidd
```

저장소 루트에서 아래 명령을 실행하면 개인 스킬 폴더에 설치합니다. 기존 `wsidd`가 있으면 멈추므로, 기존 사용자는 변경 내용을 먼저 비교해 주세요.

```powershell
$wsiddSkillBase = if ($env:CODEX_HOME) {
    Join-Path $env:CODEX_HOME 'skills'
} else {
    Join-Path $env:USERPROFILE '.codex\skills'
}
$wsiddSource = Join-Path (Get-Location).Path 'skills\wsidd'
$wsiddTarget = Join-Path $wsiddSkillBase 'wsidd'
if (-not (Test-Path -LiteralPath (Join-Path $wsiddSource 'SKILL.md'))) {
    throw '저장소 루트에서 실행해 주세요.'
}
if (Test-Path -LiteralPath $wsiddTarget) {
    throw '기존 wsidd가 있습니다. 변경 내용을 비교한 뒤 갱신해 주세요.'
}
New-Item -ItemType Directory -Path $wsiddSkillBase -Force | Out-Null
Copy-Item -LiteralPath $wsiddSource -Destination $wsiddTarget -Recurse
```

설치 후 새 작업에서 `$wsidd`를 호출합니다. 목록에 나타나지 않으면 사용 중인 클라이언트의 스킬 목록을 새로 고치거나 앱을 다시 엽니다. Markdown 지침이므로 별도 서버나 Python 실행 의존성은 없습니다.

## 파일 구성

```text
skills/wsidd/
  SKILL.md
  agents/openai.yaml
  references/evidence-rubric.md
```

설치·갱신할 때 `skills/wsidd` 전체를 사용합니다. 참고 파일을 함께 복사해야 판정 기준을 읽을 수 있습니다.

## 배포 검증

2026-09-16 기준 설치된 스킬에서 배포본을 만들었습니다. `skill-creator`의 구조 검사와 UTF-8·YAML·상대 링크 검사를 통과했습니다. 스킬 파일 3개의 SHA-256 해시가 설치된 원본과 일치했습니다. 검사는 패키지의 구조와 복사 상태를 확인하며 프로젝트 상태 판단의 정확도를 측정한 성능 시험은 아닙니다.
