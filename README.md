# actions-lock-lab

GitHub Actions 워크플로 잠금 파일(`.github/workflows/actions.lock`)이 업스트림 태그 이동을 어떻게 다루는지 재현하는 실험 레포다.

- `act/`: 업스트림 액션 역할. 릴리스 커밋을 main 밖의 곁가지로 만들고 메이저 태그 `v1`을 옮긴다(azure/login, cloudflare/wrangler-action과 같은 방식).
- `wrap/`: 남이 만든 composite 액션 역할. 안에서 `act@v1`을 메이저 태그로 부른다.
- `.github/workflows/direct.yml`: `act`를 직접 쓴다.
- `.github/workflows/transitive.yml`: `wrap`을 통해 `act`를 간접으로 쓴다.

Reproduction lab for how GitHub Actions workflow lockfiles handle upstream tag moves.

main 에 들어간 개발 커밋 예시 (v1.1.0 릴리스 전).

## thirdparty.yml

실제 서드파티 composite 액션(`svrooij/azure-static-web-app-deploy-action@v1.3.1`, 안에서 `azure/login@v3` 호출)을 쓰는 워크플로다. 단계는 `if: false` 라 실행되지 않고, 잡 준비 단계의 잠금 검사만 본다.
2026-11-12 에 `azure/login@v3` 의 고정 커밋을 2026-09-09 무렵의 값(7ddb5af, v3.0.2)으로 바꿔 실행이 거부되는 것을 확인했고, `gh actions-lock --accept-moved` 로 현재 값(a641126, v3.1.0)으로 되돌렸다.
