# Stateboard 동기화 프롬프트

[English](stateboard-sync-prompt.md) · [中文](stateboard-sync-prompt.zh.md)

Stateboard의 무설치 진입점입니다. 아래 프롬프트를 복사하고 대괄호 안의 내용을 바꿔 사용하세요.

```text
다음 프로젝트 또는 대화 컨텍스트를 프로젝트 상태 보드로 정리한 뒤, 내가 지정한 대상으로 동기화해 주세요.

정리할 내용:
[예: 내가 제공할 수 있거나 읽을 수 있는 Codex / ChatGPT / Claude / DeepSeek / WorkBuddy의 최근 60일 대화, 현재 프로젝트, 프로젝트 폴더, 기존 TODO, 붙여 넣은 여러 프로젝트 대화]

동기화 대상:
[예: Dida/TickTick, Notion, Google Calendar, Feishu/Lark, DingTalk, WeCom, Markdown만 출력]

대상 위치:
[예: Dida/TickTick의 "Project Control" 목록, Notion 페이지/데이터베이스, "XXX라는 새 목록 만들기", Markdown만이면 "이 스레드에 바로 답변"]

자동 업데이트:
[필요 없음 / 매일 HH:MM / 매주 요일 HH:MM. 명확한 시간이 없으면 "필요 없음"이라고 쓰기]

규칙:
- 읽거나 검색할 수 있거나 내가 제공한 내용만 사용한다. 보이지 않는 대화나 프로젝트 자료가 있으면 무엇이 부족한지 알려 준다.
- 먼저 근거로 프로젝트 상태를 판단한다. 대화 기록을 그대로 많은 작업으로 쪼개지 않는다.
- 기본적으로 실제 프로젝트마다 프로젝트 상태 작업 1개만 생성하거나 업데이트한다. 현재 진행 상황, 위험/블로커, 다음 단계, 근거를 포함한다.
- 각 작업에는 정말 유용한 다음 단계 3-5개만 남긴다.
- 쓰기 전에 기존 작업을 검색한다. 같은 프로젝트의 상태 작업이 이미 있으면 중복 생성하지 말고 업데이트한다.
- 현재 환경에서 대상 도구에 쓸 수 없으면, 복사하기 쉬운 Markdown 버전을 출력하고 블로커를 설명한다.
- 자동 업데이트를 요청했지만 빈도와 정확한 시간이 모두 없으면 먼저 질문한다. 기본 시간을 가정하지 않는다. 현재 환경에서 자동화를 만들 수 없으면 만들었다고 주장하지 말고 복사 가능한 설정 안내를 제공한다.
- token, webhook secret, license key, private credential, private destination identifier를 쓰지 않는다.
- 내가 명시적으로 이중 언어 출력을 요청하지 않는 한, 내 요청 언어로 답하고 같은 언어로 대상 내용을 작성한다.
- 완료 후 무엇을 만들었는지, 무엇을 업데이트했는지, 어떻게 검증했는지, 아직 확인이 필요한 것이 무엇인지 알려 준다.
```

## 최소 테스트 입력

```text
정리할 내용:
현재 Stateboard 프로젝트 또는 <your-project-path>의 프로젝트

동기화 대상:
Dida/TickTick

대상 위치:
Project Status Test라는 새 목록 만들기

자동 업데이트:
필요 없음
```
