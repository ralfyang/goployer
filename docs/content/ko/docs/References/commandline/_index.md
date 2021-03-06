---
title: "명령어 인자"
linkTitle: "명령어 인자"
weight: 10
---

<br>

프로젝트 시작:
* [goployer init](#goployer-init) - goployer 프로젝트 구조 생성
* [goployer add](#goployer-add) - 새로운 goployer 매니페스트 파일 생성

<br>

배포 정보 조회 및 수정:
* [goployer status](#goployer-status) - 특정 배포 관련 정보 조회

<br>

전체 배포 과정 실행: 
* [goployer deploy](#goployer-deploy) - 배포 실행 
* [goployer delete](#goployer-delete) - 이전 배포 삭제


## goployer init
- 프로젝트 구조 생성
```
Examples:
  # Minimum argument
  goployer init

  # See log
  goployer init --log-level=debug

Options:
      --log-level string                Level of logging
```
- 프로젝트 파일들은 현재 디렉토리에 생성됩니다.
  - manifests
  - scripts
  - metric.yaml
<br>

## goployer add
-  새로운 goployer 매니페스트 파일 생성
```
Examples:
  # Minimum argument
  goployer add 

  # You can specify application name from command
  goployer add hello

Options:
      --log-level string                Level of logging
```
<br>

## goployer status
-  특정 배포 관련 정보 조회
```
Examples:
  # Minimum argument
  goployer status hello --region=ap-northeast-2

Options:
      --region string                  Region of autoscaling group
```
<br>

## goployer deploy
-  새로운 어플리케이션 배포 실행

```

Examples:
  # Minimum argument
  goployer deploy --manifest=configs/hello.yaml --stack=artd --region=ap-northeast-2

  # Use manifest from s3
  goployer deploy --manifest=s3://goployer/manifest/hello.yaml --manifest-s3-region=ap-northeast-2 --stack=artd --region=ap-northeast-2

  # Turn off slack notification
  goployer deploy --manifest=configs/hello.yaml --stack=artd --region=ap-northeast-2 --slack-off=true

  # Control polling interval for healthcheck
  goployer deploy --manifest=configs/hello.yaml --stack=artd --region=ap-northeast-2 --polling-interval=30s

Options:
  -m, --manifest string                 The manifest configuration file to use. (required)
      --stack string                    stack that should be deployed.(required)
      --manifest-s3-region string       Region of bucket containing the manifest configuration file to use. (required if –manifest starts with s3://)
      --ami string                      Amazon AMI to use.
      --ansible-extra-vars string       Extra variables for ansible
      --assume-role string              The Role ARN to assume into.
      --disable-metrics                 Disable gathering metrics.
      --env string                      The environment that is being deployed into.
      --extra-tags string               Extra tags to add to autoscaling group tags
      --force-manifest-capacity         Force-apply the capacity of instances in the manifest file
      --log-level string                Level of logging
      --override-instance-type string   Instance Type to override
      --polling-interval duration       Time to interval for polling health check (default 60s)
      --region string                   The region to deploy into, if undefined, then the deployment will run against all regions for the given environment.
      --release-notes string            Release note for the current deployment
      --release-notes-base64 string     Base64 encoded string of release note for the current deployment
      --slack-off                       Turn off slack alarm
      --timeout duration                Time to wait for deploy to finish before timing out (default 60m)
      --auto-apply                      Apply command without confirmation from local terminal
```
<br>

### 추가 정보
* 만약 `--ami`를 명시한 경우에는 stack에 하나의 리전만 있거나 `--region`을 통해 리전을 명시해 주어야 합니다.

## goployer delete
- 이전 배포 버전 삭제
```

Examples:
  # Minimum argument
  goployer delete --manifest=configs/hello.yaml --stack=artd --region=ap-northeast-2

  # Use manifest from s3
  goployer delete --manifest=s3://goployer/manifest/hello.yaml --manifest-s3-region=ap-northeast-2 --stack=artd --region=ap-northeast-2

  # Control polling interval for healthcheck
  goployer delete --manifest=configs/hello.yaml --stack=artd --region=ap-northeast-2 --polling-interval=30s

Options:
  -m, --manifest string                 The manifest configuration file to use. (required)
      --stack string                    stack that should be deployed.(required)
      --manifest-s3-region string       Region of bucket containing the manifest configuration file to use. (required if –manifest starts with s3://)
      --region string                   The region to deploy into, if undefined, then the deployment will run against all regions for the given environment.
      --assume-role string              The Role ARN to assume into.
      --disable-metrics                 Disable gathering metrics.
      --env string                      The environment that is being deployed into.
      --log-level string                Level of logging
      --polling-interval duration       Time to interval for polling health check (default 60s)
      --timeout duration                Time to wait for deploy to finish before timing out (default 60m)
      --auto-apply                      Apply command without confirmation from local terminal
```
<br>
