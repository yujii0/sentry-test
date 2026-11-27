# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 레포 성격

빌드·테스트·린트 대상 코드가 없는 **문서 전용 레포**다. Sentry 이슈 분석과 주간 모니터링 보고를 Claude Code로 자동화하기 위한 절차서와 설정을 담는다. 이 레포는 동시에 Sentry Alert가 GitHub Issue를 자동 생성하는 **이슈 레포**(`yujii0/sentry-test`)다.

## 구조와 문서 간 관계

- `docs/sentry-automation-plan.md` — 전체 계획서 (목표, 라벨 정책, 권한, Notion 연동, 부록 A에 Routine 프롬프트)
- `tasks/sentry-issue.md` — **이슈 정리 절차**. `Triage: new` GitHub 이슈를 Sentry 조회 + 코드 레포 읽기 분석으로 표준 템플릿 본문으로 교체. 스킬 `sentry-issue`가 읽음
- `tasks/sentry-weekely-report.md` — **주간 보고 절차**. Sentry 7일 데이터로 Notion [주간 모니터링 보고] DB에 프로젝트별 페이지 생성. 스킬 `weekly-sentry-report`가 읽음 (파일명 `weekely` 오타는 참조 중이므로 임의로 바꾸지 않는다)
- `tasks/sentry-projects.md` — **레지스트리**. Sentry 조직, 이슈 레포, Slack 채널, 프로젝트 slug → 코드 레포 매핑표. 두 절차서가 공통으로 읽는 유일한 기준

클라우드 Routine은 이 레포에 커밋된 `tasks/` 파일만 읽는다. 로컬 반자동 실행용 `~/.claude/sentry-projects.md`는 별도 파일이므로 프로젝트가 추가·변경되면 **양쪽을 함께 갱신**한다.

절차서를 고치면 계획서의 해당 설명(특히 부록 A 프롬프트, 5장 권한 표)과 어긋나지 않는지 같이 확인한다.

## GitHub 접근 규칙

- GitHub 작업은 GitHub 커넥터(MCP)를 쓰지 않고 환경변수 `GH_TOKEN`으로 REST API를 직접 호출한다.
- 헤더: `Authorization: Bearer $GH_TOKEN`, `Accept: application/vnd.github+json`
- 기준 주소: `https://api.github.com`, 저장소는 `yujii0/sentry-test`.
- 토큰 값은 출력, 파일, 커밋, 채팅 어디에도 쓰지 않는다.
- 쓰기 요청이 프록시에서 막히면 우회하지 말고, 막혔다는 사실과 응답 메시지를 보고한다.

## Notion 접근 규칙

- Notion은 MCP를 쓰지 않고 REST API로 호출한다.
- 헤더: `Authorization: Bearer $NOTION_TOKEN`, `Notion-Version: 2022-06-28`, `Content-Type: application/json`
- 기준 주소는 `https://api.notion.com/v1`이다.
- 토큰 값은 출력, 파일, 커밋, 채팅 어디에도 쓰지 않는다.

## 핵심 운영 규칙 (절차서 수정 시 유지)

- 쓰기 가능한 레포는 이 레포 하나뿐이다. `tasks/sentry-projects.md`의 코드 레포(`pj.antiscam.co.kr` 등)는 읽기 전용이며 수정·커밋·push·PR·이슈·코멘트 금지.
- 이슈 정리는 기존 이슈 본문만 수정한다. 새 이슈 생성, 닫기, 제목 변경, 코멘트 금지. 처리 대상은 open + `Triage: new` 이슈뿐이다.
- 상태 라벨은 이슈당 하나만 유지한다: `Triage: new` → `Triage: ai-drafted`(Claude) → `Triage: approved`(관리자만). Claude는 `approved`나 분류 라벨을 붙이지 않는다.
- 숫자·사실은 Sentry/Notion 조회값만 쓴다. 불확실하면 `(추정)`, `(확인 필요)`, `-` 로 표시하고 요약에 사유를 적는다.
- 개인정보(이메일, IP, 사용자 ID, 토큰 등)는 본문에 쓰지 않고 `[마스킹됨]`으로 대체한다.
- Notion은 기존 페이지 수정·삭제와 체크박스 체크 금지. 새 페이지 생성, 이슈 행 추가, 새 페이지 뷰 필터 설정만 허용한다. 주간 보고는 MCP가 아니라 REST API(`NOTION_TOKEN` 환경변수)를 쓰며 토큰 값은 어디에도 기록하지 않는다.
- 주간 보고 날짜(`RUN_DATE`)는 KST 기준 실행 당일이며 고정값을 쓰지 않는다.

## 참고

- 현재 확정된 프로젝트는 12개 중 11개이고 `hp-couponwallet`은 코드 레포 미확정(`?`)이다. `?`·`-`는 코드 분석 없이 Sentry 데이터만으로 초안을 쓰고 `(코드 미확인)`을 붙인다.
- 이슈 본문 형식(섹션·분량 상한·마크다운 규칙)은 `tasks/sentry-issue.md` 4장이 기준이다. 형식 예시를 다른 곳에 복제하지 않는다.
