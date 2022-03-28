- port-forward and open in browser
	- ```sh
	  kubectl -n argo port-forward svc/argo-server 2746:2746
	  # open https://localhost:2746
	  ```
- `tmux` 사용하기
	- ```sh
	  tmux new-session 'kubectl -n argo port-forward svc/argo-server 2746:2746' \; \
	    split-window 'open https://localhost:2746'
	  ```