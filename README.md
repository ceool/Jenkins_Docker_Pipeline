# Jenkins_Docker_Pipeline
젠킨스와 도커를 활용하여 CI/CD 파이프라인 구축을 해보았습니다.<br>
예제로, 도커에서 Terraform 컨테이너를 띄운 뒤 AWS 보안그룹을 생성합니다.
![main](https://user-images.githubusercontent.com/62891711/111121890-9413dc80-85b0-11eb-8486-f3784724dc73.png)

### 구성도(Docker Out of Docker)
젠킨스 내부에서 도커를 사용하기 위하여 /var/run/docker.sock 볼륨을 공유합니다.<br>
(이러한 방법은 Docker in Docker의 privileged mode의 보안 취약점을 해결할 수 있습니다.)
![2](https://user-images.githubusercontent.com/62891711/111122433-654a3600-85b1-11eb-839e-a467cce1586d.png)

### Jenkinsfile, credentials 수정
1. 테라폼 예제를 사용하기 위해선, Jenkinsfile의 aws credentials 경로를 수정해야합니다.
```
-v /root/jenkins/jenkins_home/.aws:/root/.aws
```
<br>

2. credentials 파일의 내용을 본인의 키 값으로 변경합니다.

```
[default]
aws_access_key_id = YOUR_ACCESS_KEY_ID
aws_secret_access_key = YOUR_SECRET_ACCESS_KEY_ID
```
