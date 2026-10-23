# REA 설치 준비

REA(Reverse Engineer Anything)를 설치하기 전에 확인할 내용을 한 장에 정리했습니다.
공식 저장소는 [github.com/morluto/rea](https://github.com/morluto/rea) 하나뿐입니다.

> 2026.10.23 기준으로 공개된 기사와 팩트체크를 정리한 내용입니다. 설치 직전에 공식 README와 한 번 더 대조하세요.

---

## 1. 한 줄 요약

AI 에이전트(Claude Code 등)가 소스코드 없이 완성된 프로그램을 분석하게 해주는 연결 도구입니다. 직접 디컴파일을 하지는 않고, Ghidra·Hopper·IDA 같은 기존 분석 도구를 에이전트가 쓸 수 있게 묶어줍니다.

| 항목 | 내용 |
|---|---|
| 형태 | MCP 서버 + CLI |
| 라이선스 | MIT (무료) |
| 분석 대상 | 일반 실행파일, JavaScript·Electron 앱, .NET 프로그램 |
| 설치 명령 | `npx rea-agents setup` |

---

## 2. 필요한 프로그램

| 구분 | 프로그램 | 비고 |
|---|---|---|
| 필수 | Node.js 22.19 이상 | `node -v`로 버전 확인 |
| 필수 | AI 에이전트 1개 | Claude Code, Cursor, Codex, Gemini CLI 중 하나 |
| 실행파일 분석 시 | Hopper / Ghidra / IDA 중 1개 | JS·.NET만 볼 거라면 없어도 됨 |
| 자동 설치될 수 있음 | Homebrew, Hopper | Mac에서 필요할 때 설치 스크립트가 직접 설치 |

---

## 3. 설치 전 체크리스트

- [ ] 받는 곳이 `github.com/morluto/rea` 공식 저장소인지 확인
- [ ] 다른 사이트에서 받은 `REA.exe` 같은 설치파일은 쓰지 않기 (README에 Windows 설치 프로그램은 없음)
- [ ] `node -v` 결과가 22.19 이상인지 확인
- [ ] 쓰려는 AI 에이전트가 설치되어 있고 로그인되어 있는지 확인
- [ ] 분석할 대상이 실행파일이라면 Ghidra·Hopper·IDA 중 하나가 준비되어 있는지 확인
- [ ] 회사 PC라면 IT·보안팀에 외부 프로그램 설치가 허용되는지 확인
- [ ] 분석하려는 프로그램이 라이선스·이용약관상 분석이 허용된 대상인지 확인

---

## 4. 보안 확인 사항

**설치하면 내 PC에서 바뀌는 것**

- Claude Code 설정에 REA 서버가 등록되고, 스킬 폴더에 REA 스킬이 복사됩니다. 이후 여는 모든 프로젝트에서 REA를 쓸 수 있게 됩니다.
- Claude Desktop이나 Cursor가 깔려 있으면 그쪽 설정도 같이 바뀝니다.
- 필요하면 Homebrew와 Hopper를 직접 설치합니다.

**권장하는 대응**

- 업무용 Claude 설정과 분리해서 쓰기. 별도 설정 폴더를 지정해 실행하면 기존 설정을 건드리지 않습니다.
  ```bash
  CLAUDE_CONFIG_DIR=~/.claude-rea claude
  ```
- 에이전트는 설치 후에도 파일·터미널·네트워크 접근 권한을 그대로 갖습니다. 고객 자료나 계약서가 있는 폴더에서는 실행하지 않습니다.
- 출처가 확인되지 않은 프로그램을 분석할 때는 업무용 PC가 아니라 별도 PC나 가상머신에서 진행합니다.
- 스타 수나 "공식 배포" 같은 홍보 문구만 보고 링크를 누르지 않습니다. 인기 저장소를 흉내 낸 가짜 복제본이 실제로 돌고 있습니다.

---

## 5. 설치 순서

1. 위 체크리스트를 모두 확인합니다.
2. 터미널에서 Node.js 버전을 확인합니다. `node -v`
3. 설치 명령을 실행합니다. `npx rea-agents setup`
4. 설치 중 무엇을 바꾸는지 화면에 나오는 안내를 끝까지 읽고 진행합니다.
5. 에이전트를 다시 시작하고, 분석이 허용된 테스트용 프로그램으로 먼저 동작을 확인합니다.

---

**참고 자료**
[GitHub 저장소](https://github.com/morluto/rea) ·
[팩트체크 (pasqualepillitteri.it)](https://pasqualepillitteri.it/en/news/23845/rea-reverse-engineer-anything-github-true-false) ·
[UX Planet 해설](https://uxplanet.org/reverse-engineer-anything-what-the-viral-github-repo-actually-does-c5ea949123a5) ·
[all-ai.de](https://www.all-ai.de/news/news26top/rea-github-erfolg)
