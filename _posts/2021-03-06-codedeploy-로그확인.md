---
title: "CodeDeploy 로그 확인"
categories: aws
tags: aws codedeploy
---

## 에이전트 로그 확인
```
$ less /var/log/aws/codedeploy-agent/codedeploy-agent.log
```

## 배포로그 확인
```
$ less /opt/codedeploy-agent/deployment-root/{deployment-group-id}/{deployment-id}/logs/scripts.log
```

## 참고
- [AWS CodeDeploy 배포 타겟인 EC2/온프레미스 배포에 대한 로그 보기](https://gamoo12.tistory.com/208)
- [CodeDeploy 에이전트 설치](https://docs.aws.amazon.com/ko_kr/codedeploy/latest/userguide/codedeploy-agent-operations-install.html)
- [CloudWatch 로그 에이전트 설치하여 로그 확인 방법](https://aws.amazon.com/ko/blogs/devops/view-aws-codedeploy-logs-in-amazon-cloudwatch-console/)