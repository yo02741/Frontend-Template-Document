# Gitlab CI

1. `apt-get` 安裝 `Github Runner`

```shell
curl -L https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.deb.sh | sudo bash
```

```shell
sudo apt-get install gitlab-runner
```

2. 向 `GitLab Server` 完成註冊

```shell
sudo gitlab-runner register
```

輸上 `URL` 以及 `token`

![](https://hackmd.io/\_uploads/BJnyIxacn.png)

完成後重整一下就會看到註冊好的 `Github Runner`

![](https://hackmd.io/\_uploads/HJH-Lxa5h.png)

3. 定義 `Github CI Pipeline`

```yaml
stages:
  - testCI
  - build
  # - test

testCI:
  image: node:16-alpine
  stage: testCI
  only:
    - testCI
  script:
    - node -v
    - echo "TEST CI !"

build-stage:
  image: node:16-alpine
  stage: build
  only:
    - stage
  script:
    - apk add git
    - npm install
    - npm run build:stage
  artifacts:
    expire_in: 2 week
    paths:
      - dist

build-production:
  image: node:16-alpine
  stage: build
  only:
    - production
  script:
    - apk add git
    - npm install
    - npm run build
  artifacts:
    expire_in: 2 week
    paths:
      - dist
# testing:
#   image: node:16-alpine
#   stage: test
#   script:
#     - npm install
#     - npm run test:unit

```

4. 推上指定分支，觸發對應的 Job

![](https://hackmd.io/\_uploads/B1\_ZfZ653.png)

![](https://hackmd.io/\_uploads/r1-xz-pqn.png)
