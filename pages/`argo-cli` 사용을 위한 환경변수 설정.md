- TODO 오류가 없는지 확인 필요
  :LOGBOOK:
  CLOCK: [2022-03-28 Mon 15:30:37]--[2022-03-28 Mon 15:30:38] =>  00:00:01
  :END:
- ```sh
  # .envrc
  export ARGO_SERVER='localhost:2746' 
  export ARGO_HTTP1=true  
  export ARGO_SECURE=true
  export ARGO_BASE_HREF=
  export ARGO_TOKEN="Bearer $(kubectl -n argo get secret $(kubectl -n argo get sa argo -o jsonpath={.secrets[0].name}) -o jsonpath={.data.token} | base64)"
  export ARGO_NAMESPACE=argo ;# or whatever your namespace is 
  export KUBECONFIG=/dev/null ;# recommended
  export ARGO_INSECURE_SKIP_VERIFY=true
  ```