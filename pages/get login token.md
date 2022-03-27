- ```sh
  echo "Bearer $(kubectl -n argo get secret $(kubectl -n argo get sa argo -o jsonpath={.secrets[0].name}) -o jsonpath={.data.token} | base64)"
  ```
