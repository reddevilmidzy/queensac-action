# queensac-action

`queensac-action`은 [queensac][queensac-repo] Rust CLI를 GitHub Action 형태로 제공하는 저장소입니다. 워크플로우에서 이 액션을 실행하면 대상 레포지토리를 복제하고, 문서 속 모든 HTTP(S) 링크를 검사하고, 필요한 경우 자동으로 PR을 생성합니다.

[English](README.md) | [한국어](README.ko.md)

## 작동 방식

- `git2`를 활용해 레포지토리 트리를 순회하며 링크를 추출합니다.
- `reqwest` 기반 검사기로 링크 유효성, 리디렉션, GitHub 파일 이동 여부를 판별합니다.
- `octocrab`과 GitHub App 인증을 사용해 수정 내용을 자동 커밋·푸시하고 PR을 개설합니다.

## 사용법

```yaml
- name: 👑 Run queensac
  uses: reddevilmidzy/queensac-action@v1
  with:
    repo: https://github.com/${{ github.repository }}
    branch: main
    dry-run: false
    github_app_id: ${{ secrets.QUEENSAC_APP_ID }}
    github_app_private_key: ${{ secrets.QUEENSAC_APP_PRIVATE_KEY }}
```

### 입력 값

| 이름 | 필수 | 설명 |
| --- | --- | --- |
| `repo` | 선택 | 검사할 GitHub 레포지토리 URL, 기본값은 워크플로우 레포지토리입니다. |
| `branch` | 선택 | 검사 및 PR 베이스로 사용할 브랜치 (기본값 `main`). |
| `dry-run` | 선택 | `true`일 경우 PR 생성 없이 결과만 출력합니다. |
| `github_app_id` | 선택 | GitHub App 인증에 사용할 앱 ID. |
| `github_app_private_key` | 선택 | GitHub App용 PEM 프라이빗 키. |

## 라이선스

Apache-2.0. 자세한 내용은 [LICENSE](LICENSE)를 확인하세요.

[queensac-repo]: https://github.com/reddevilmidzy/queensac
