- [kubernetes - How to view the permissions/roles associated with a specific service account in k8s? - Stack Overflow](https://stackoverflow.com/questions/54602224/how-to-view-the-permissions-roles-associated-with-a-specific-service-account-in)
	- ```sh
	  kubectl get rolebinding,clusterrolebinding \
	    --all-namespaces \
	    -o jsonpath='{range .items[?(@.subjects[0].name=="SERVICE_ACCOUNT_NAME")]}[{.roleRef.kind},{.roleRef.name}]{end}'
	  ```
	- `\t`으로 구분
	- ```sh
	  kubectl get rolebinding,clusterrolebinding \
	    --all-namespaces \
	    -o jsonpath='{range .items[?(@.subjects[0].name=="SERVICE_ACCOUNT_NAME")]}{.roleRef.kind}{"\t"}{.roleRef.name}{"\n"}{end}'
	  ```