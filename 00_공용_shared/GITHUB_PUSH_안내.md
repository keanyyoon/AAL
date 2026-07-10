# GitHub 새 프로젝트 생성 & Push 안내 (Glim / AAL)

이 세션에서는 GitHub 인증·커넥터가 없고, 폴더의 `.git/index.lock`(잔여 잠금)을 삭제할 권한이 없어 원격 저장소를 직접 만들지 못했습니다.
아래 명령을 **본인 컴퓨터 터미널**에서 실행하면 새 저장소가 생성·업로드됩니다. (로컬에서는 lock 삭제가 됩니다)

## 방법 A — GitHub CLI (`gh`) 설치돼 있으면 (가장 간단)
```bash
cd "~/Claude/Projects/[AAL] AI Agent Learning"

# 1) 잔여 잠금 제거 + 최신 상태 커밋
rm -f .git/index.lock
git add -A
git -c user.email="yym0@creverse.com" -c user.name="Youngmin" \
  commit -m "Glim POC: 세션선택+학습씬, 세계관 v2(어둠속의 빛), 브랜딩/UX 업데이트"

# 2) 새 Private 저장소 생성 + 업로드 (한 번에)
gh repo create AAL-Glim --private --source=. --remote=origin --push
```

## 방법 B — github.com에서 빈 저장소 먼저 만든 뒤 push
1. github.com → New repository → 이름 예: `AAL-Glim` (Private) → 생성(README 체크 해제).
2. 터미널:
```bash
cd "~/Claude/Projects/[AAL] AI Agent Learning"
rm -f .git/index.lock
git add -A
git -c user.email="yym0@creverse.com" -c user.name="Youngmin" \
  commit -m "Glim POC + 세계관 v2 + 브랜딩/UX"
git branch -M main
git remote add origin https://github.com/<본인계정>/AAL-Glim.git   # 이미 있으면 set-url
git push -u origin main
```

## 방법 C — 웹 업로드 (git 없이)
- 첨부 `AAL_Glim_project.zip`을 풀어서, github.com의 새 저장소 "uploading an existing file"로 드래그·드롭.

## 참고
- 현재 로컬 저장소에는 초기 커밋(`b6ef3ea`, 44개 파일)이 있고, 이후 산출물은 위 `git add -A`로 함께 커밋됩니다.
- 대용량이 걱정되면 `AAL_Glim_project.zip`은 커밋에서 제외하세요(.gitignore에 `*.zip` 추가).
- 자동 생성·push를 원하시면 claude.ai 커넥터 설정에서 GitHub를 연결해 주세요. 다음부터는 제가 직접 처리할 수 있습니다.
