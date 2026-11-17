# Craft Anything 설치 준비

Craft Anything을 설치하기 전에 확인할 내용을 한 장에 정리했습니다.
공식 저장소는 [github.com/storytold/craft-anything](https://github.com/storytold/craft-anything) 하나뿐입니다.

> 2026.11.17 기준 공식 README를 직접 읽고 정리했습니다. 초기 알파 단계라 내용이 자주 바뀌니, 설치 직전에 README와 한 번 더 대조하세요.

---

## 1. 한 줄 요약

웹사이트·앱·게임을 지정하고 원하는 바를 말로 설명하면, AI 에이전트가 원본을 관찰한 뒤 새 프로젝트로 다시 만들어주는 도구입니다. ArtCraft 팀이 Rust로 만들었습니다.

| 항목 | 내용 |
|---|---|
| 형태 | 데스크톱 앱 + CLI + MCP 서버 |
| 라이선스 | MIT 또는 Apache-2.0 (무료) |
| 단계 | 초기 알파 (2026.10.31 저장소 생성) |
| 대상 | 웹사이트, 데스크톱·모바일 앱, 게임, 펌웨어 등 |
| 주 에이전트 | Claude Code (내 PC에 로그인된 계정을 그대로 사용) |

**작업 흐름**

1. **Study** : 원본의 화면, 동작, 구조를 살펴봅니다.
2. **Build** : 에이전트가 요청한 언어·프레임워크로 새 프로젝트를 만듭니다.
3. **Check** : 결과물을 원본과 비교해 다른 점을 뽑습니다.
4. **Ready** : 결과를 열어보고, 수정 요청을 하면 다시 다듬습니다.

**두 가지 모드**

| 모드 | 동작 |
|---|---|
| Clean room (기본) | 원본의 코드·파일·페이지 소스를 읽지 않고, 보이는 화면과 동작만으로 작업 |
| Deep | 모든 분석 도구 사용. 개인적 용도 전제 |

---

## 2. REA와 다른 점

| | REA | Craft Anything |
|---|---|---|
| 하는 일 | 프로그램을 **분석**해서 설명 | 원본을 관찰해 **새로 만들어냄** |
| 형태 | 에이전트에 붙이는 연결 도구 | 자체 앱이 있는 완성형 도구 |
| 설치 | `npx` 명령 한 줄 | 설치파일 다운로드 |
| 추가 프로그램 | Ghidra·Hopper·IDA 필요 | 기본 사용에는 불필요 |
| 성숙도 | 0.3.0 이상 배포 | 초기 알파 |

---

## 3. 필요한 프로그램

| 구분 | 프로그램 | 비고 |
|---|---|---|
| 필수 | Craft Anything 설치파일 | 공식 Releases 페이지에서 OS에 맞게 다운로드 |
| 필수 | 코딩 에이전트 1개 | Claude Code 권장. 미리 로그인되어 있어야 함 |
| 선택 | AI API 키 | 질문·분석 기능용 (Anthropic, OpenAI, OpenRouter, xAI) |
| 선택 | fal.ai 키 | 이미지·3D 모델 생성 기능을 쓸 때만 |
| 소스 빌드 시 | Rust 1.97 이상 | 설치파일을 쓰면 필요 없음 |

**OS별 설치파일**

| OS | 형식 | 비고 |
|---|---|---|
| Windows | `.msi` 또는 포터블 `.zip` | 코드 서명됨. 포터블은 설정이 앱 폴더에 저장 |
| macOS | `.dmg` | 서명·공증 완료. 0.2.0부터 앱에 CLI 포함 |
| Linux | AppImage, `.deb`, `.rpm`, Flatpak | Flatpak은 브라우저를 띄우지 못해 웹사이트 분석 불가 |

---

## 4. 설치 전 체크리스트

- [ ] 받는 곳이 `github.com/storytold/craft-anything`의 Releases 페이지인지 확인
- [ ] 받은 파일을 릴리스에 함께 올라온 `SHA256SUMS.txt`와 대조
- [ ] Claude Code가 설치되어 있고 로그인되어 있는지 확인
- [ ] 회사 PC라면 IT·보안팀에 외부 프로그램 설치가 허용되는지 확인
- [ ] 다시 만들려는 대상이 내가 소유했거나 분석 허락을 받은 것인지 확인
- [ ] 결과물을 외부에 공개하거나 고객에게 전달할 계획이라면 법무 검토를 먼저 받기
- [ ] 알파 단계임을 감안해 업무 자료가 없는 폴더·PC에서 먼저 시험

---

## 5. 보안 · 법적 확인 사항

**설치하면 내 PC에서 생기는 것**

- 새 프로젝트는 기본적으로 `문서/Craft Anything` 폴더에 만들어집니다. 설정에서 바꿀 수 있습니다.
- `craft-anything-cli setup`을 실행하면 코딩 에이전트 앱 설정에 Craft Anything이 연결됩니다.

**알고 써야 할 위험**

- **만드는 과정에서 외부 코드가 실행됩니다.** 에이전트가 새 프로젝트의 부품(npm 패키지 등)을 설치할 때, 그 패키지가 내 PC에서 코드를 실행할 수 있습니다. 처음 보는 종류의 명령은 실행 전에 물어봅니다.
- **"Always allow"는 누르지 않는 편이 안전합니다.** npm에 대해 한 번 허용하면 이후 모든 npm 명령이 묻지 않고 실행됩니다.
- **Clean room은 보안 장치가 아닙니다.** 앱이 스스로 지키는 규칙일 뿐, 에이전트는 내 계정 권한 그대로 PC에서 움직입니다.
- **Claude Code 사용분은 내 계정에 잡힙니다.** 사용량과 약관 책임 모두 본인 계정 기준입니다.

**법적으로 조심할 부분**

- README는 본인 소유이거나 허락받은 소프트웨어만 대상으로 삼으라고 명시합니다. DRM·로그인·안티치트 우회는 하지 않는다고 밝히고 있습니다.
- 로고·사진·문구는 소유권이나 사용 허락을 확인해 주지 않으면 복사하지 않도록 되어 있습니다.
- AI가 기존 제품을 보고 다시 만든 결과물의 저작권 문제는 아직 정리되지 않은 영역입니다. 다른 회사의 사이트나 앱을 본떠 업무에 쓰는 것은 법무 확인 없이 진행하지 않습니다.

---

## 6. 설치 순서

1. 위 체크리스트를 모두 확인합니다.
2. [Releases 페이지](https://github.com/storytold/craft-anything/releases/latest)에서 OS에 맞는 설치파일을 받습니다.
3. `SHA256SUMS.txt`로 파일이 원본과 같은지 확인한 뒤 설치합니다.
4. 설치 상태를 점검합니다.
   ```bash
   craft-anything-cli doctor
   ```
5. 앱을 Simple 모드, Clean room 설정 그대로 두고, 본인 소유의 간단한 웹페이지로 먼저 시험합니다.

---

**참고 자료**
[GitHub 저장소](https://github.com/storytold/craft-anything) ·
[pbxscience 기사](https://pbxscience.com/?p=24951) ·
[ibl.ai 해설](https://ibl.ai/blog/craft-anything-clean-room-rebuild-software-moat) ·
[DeepWiki](https://deepwiki.com/storytold/craft-anything) ·
[Trendshift](https://trendshift.io/repositories/331267)
