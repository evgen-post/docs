[главная](../readme.md)

# CI/CD

## Gitlab CI

```yaml
stages:
  - dev

.run_dev_deploy: &run_dev_deploy |
  ssh -p 9506 -tt user@185.251.151.175 << EOF
  cd bitrix_sber_fm/sber/local/templates/.default/markup/
  nvm use 20.18
  git fetch
  git status
  git checkout $CI_COMMIT_SHA
  yarn
  yarn build
  exit
  EOF

run dev deploy:
  image: zedsh/alpine_ssh:latest
  stage: dev
  when: manual
  variables:
    GIT_STRATEGY: none
    GIT_SUBMODULE_STRATEGY: none
  script:
    - echo START DEPLOY DEV
    - echo "$SSH_PRIVATE_KEY" | tr -d '\r' > ~/.ssh/id_rsa
    - *run_dev_deploy
    - echo DONE DEPLOY DEV
```