Get tooling

```
brew install minikube kubernetes-cli
brew tap tektoncd/tools
brew install tektoncd/tools/tektoncd-cli
```

start cluster

```
minikube start
```

Install tekton and dashboard

```
kubectl apply --filename https://storage.googleapis.com/tekton-releases/pipeline/latest/release.yaml

kubectl apply --filename https://github.com/tektoncd/dashboard/releases/latest/download/tekton-dashboard-release.yaml

kubectl proxy --port=8080
```

Dashboard: http://localhost:8080/api/v1/namespaces/tekton-pipelines/services/tekton-dashboard:http/proxy/

kubectl apply -f ci/task/task-hello.yaml -n tekton-pipelines
tkn task start hello --dry-run
tkn task start hello
tkn taskrun logs --last -f

kubectl apply -f https://raw.githubusercontent.com/tektoncd/catalog/master/task/docker-build/0.1/docker-build.yaml -n tekton-pipelines
