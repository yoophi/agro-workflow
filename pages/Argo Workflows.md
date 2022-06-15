- 개요
  heading:: true
	- Argo Workflows 는 Kubernetes 에서 병렬 작업을 관리하기 위한 오픈소스 Container Native Workflow Engine 입니다.
	- [[Workflow]]의 각 단계를 컨테이너로 정의합니다.
	- 다단계 [[Workflow]]를 작업 시퀀스로 모델링하거나, [[DAG]]를 사용하여 작업간의 종속성을 정의할 수 있습니다.
- [Quick Start](https://argoproj.github.io/argo-workflows/quick-start/)
  heading:: true
	- 아래 명령으로 실습용 버전을 설치하고
		- ```sh
		  kubectl create ns argo
		  kubectl apply -n argo -f https://raw.githubusercontent.com/argoproj/argo-workflows/master/manifests/quick-start-postgres.yaml
		  ```
	- port-forward 를 설정하면,
		- ```sh
		  kubectl port-forward svc/argo-server 2746:2746 -n argo
		  ```
	- <https://localhost:2746> 으로 접속하여 웹 인터페이스로 사용할 수 있습니다.
	- [[Argo CLI]]를 설치하고, CLI 를 이용하여 첫번째 Workflow 를 배포할 수 있습니다.
		- ```sh
		  argo submit -n argo --watch https://raw.githubusercontent.com/argoproj/argo-workflows/master/examples/hello-world.yaml
		  ```
	- CLI 를 사용하여 목록을 확인하거나,
		- ```sh
		  argo list -n argo
		  ```
	- 상세정보를 확인하거나,
		- ```sh
		  argo get -n argo @latest
		  ```
	- 작업의 로그를 확인할 수 있습니다.
		- ```sh
		  argo logs -n argo @latest
		  ```
- Links
  heading:: true
	- {{embed [[Links]]}}