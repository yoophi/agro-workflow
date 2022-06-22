- # EmptyDir 을 이용하는 방법은 안됨.
	- POD 레벨에서 볼륨으로 마운트되는 기능.
	- step 이 달라지면, 다른 POD이 생성되므로 깨끗한 볼륨으로 생성되어 마운트 됨.
	- (차라리 PV로 처리하는게 용도에 맞을 수도 있다)
- # Artifacts 를 이용하자.
	- 전단계에서 생성한 `steps.one.outputs.artifacts.filename` 을 `input.artifacts` 로 사용할 수 있다.
	- ```yaml
	  # This example demonstrates the ability to pass artifacts
	  # from one step to the next.
	  apiVersion: argoproj.io/v1alpha1
	  kind: Workflow
	  metadata:
	    generateName: artifact-passing-
	  spec:
	    entrypoint: artifact-example
	    templates:
	    - name: artifact-example
	      steps:
	      - - name: generate-artifact
	          template: whalesay
	      - - name: consume-artifact
	          template: print-message
	          arguments:
	            artifacts:
	            - name: message
	              from: "{{steps.generate-artifact.outputs.artifacts.hello-art}}"
	  
	    - name: whalesay
	      container:
	        image: docker/whalesay:latest
	        command: [sh, -c]
	        args: ["sleep 1; cowsay hello world | tee /tmp/hello_world.txt"]
	      outputs:
	        artifacts:
	        - name: hello-art
	          path: /tmp/hello_world.txt
	  
	    - name: print-message
	      inputs:
	        artifacts:
	        - name: message
	          path: /tmp/message
	      container:
	        image: alpine:latest
	        command: [sh, -c]
	        args: ["cat /tmp/message"]
	  
	  ```