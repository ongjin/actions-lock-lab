# actions-lock-lab

GitHub Actions 워크플로 잠금 파일(`.github/workflows/actions.lock`)이 업스트림 태그 이동을 어떻게 다루는지 재현하는 실험 레포다.

- `act/`: 업스트림 액션 역할. 릴리스 커밋을 main 밖의 곁가지로 만들고 메이저 태그 `v1`을 옮긴다(azure/login, cloudflare/wrangler-action과 같은 방식).
- `wrap/`: 남이 만든 composite 액션 역할. 안에서 `act@v1`을 메이저 태그로 부른다.
- `.github/workflows/direct.yml`: `act`를 직접 쓴다.
- `.github/workflows/transitive.yml`: `wrap`을 통해 `act`를 간접으로 쓴다.

Reproduction lab for how GitHub Actions workflow lockfiles handle upstream tag moves.

main 에 들어간 개발 커밋 예시 (v1.1.0 릴리스 전).
