# Kubernetes Tutorial

도커는 어떤 환경에서든 손쉽게 앱을 실행하고, 쿠버네티스는 설정에 따라 동일한 배포 상태를 유지한다.\
쿠버네티스를 테스트할 수 있는 코드를 작성했다.

## 설치

**kubeclt 설치**

https://kubernetes.io/docs/tasks/tools/#install-with-homebrew-on-macos

kubectl은 서버를 컨트롤하는 컴퓨터에 설치해야 함

**minikube 설치**

https://minikube.sigs.k8s.io/docs/start/?arch=%2Fmacos%2Farm64%2Fstable%2Fbinary+download

minikube는 테스트를 위한 것으로 이를 이용해서 가상 머신을 만들고 클러스터가 설치된 서버처럼 쓸 수 있음

## 이미지 빌드

도커 이미지를 빌드한다.\
`-t <도커허브아이디>/<리파지토리이름>:<태그>`

```
docker build . -t gim2origin/nginx-tutorial:2
```

## 도커 허브에 이미지 푸시

```
docker push gim2origin/nginx-tutorial:2
```

## 쿠버네티스를 이용해 배포

언제든 아래 yaml 설정을 수정한 뒤 apply 해주면 배포 리소스가 마법처럼 바뀐다.

```
kubectl apply -f=deployment.yaml -f=service.yaml
```

## 실행되는 service 리스트 확인

```
kubectl get services
```

로컬 환경에서 테스트하기 위해 minikube를 이용해서 `nginx-service`라 이름 붙인 service를 실행한다.\
그러면 접근할 수 있는 임의의 URL을 제공한다.

```
minikube service nginx-service
```

## 배포 중단

```
kubeclt delete -f=deployment.yaml -f=service.yaml
```
