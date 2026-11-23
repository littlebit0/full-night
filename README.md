# full-night

사용자가 자리를 비운 동안(밤샘 등) 메인 세션이 하위 세션을 감독하며 작업을 끝까지 자율 진행하게 하는 [Claude Code](https://claude.com/claude-code) 스킬입니다. Claude 데스크톱 앱(Code 탭)의 세션 관리 도구를 기준으로 합니다.

## 하는 일

- 지정한 종료 시각까지 권한 요청을 승인한 것으로 보고 진행합니다.
- 사용자 판단이 필요해 보이는 문제는 다시 확인해, 판단 없이도 충분하면 자동 승인합니다. 남는 것만 모아 마지막에 질문·선택지·권장안으로 보고합니다.
- 하위 세션이 "빼먹었다", "못 찾았다"고 하면 다시 하라고 반려하고, 근거가 정확할 때만 승인합니다.
- 하위 세션 모델을 작업 성격에 맞춰 메인이 고릅니다.
- 사용량이 다 떨어지면 초기화 시각에 맞춰 재개 예약을 걸어, 하위 세션을 다시 시작합니다.

자세한 규칙은 [`SKILL.md`](SKILL.md)에 있습니다.

## 설치

```bash
git clone https://github.com/littlebit0/full-night ~/.claude/skills/full-night
```

## 사용

```
/full-night <종료 시각> [computer-use를 허용할 프로그램·앱...]
```

예: `/full-night 09:00`, `/full-night 06:00 Xcode`

종료 시각이 없으면 시작 전에 한 번만 묻습니다. computer-use는 Chrome과 호출 때 적은 프로그램에만 허용됩니다.

## 필요한 것

- Claude 데스크톱 앱의 세션 도구(`start_session`, `SendMessage`, `mcp__ccd_session_mgmt__*`)
- 예약 작업 도구(`mcp__scheduled-tasks__*`): 사용량 초기화 뒤 재개 예약에 씁니다.

## 라이선스

MIT
