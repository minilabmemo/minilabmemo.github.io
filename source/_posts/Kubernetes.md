---
title: "[純紀錄]Kubernetes基本操作"
tags:
  - Kubernetes
  - CLI
categories:
  - Tech.
  - deploy
  - Kubernetes

date: 2020-12-31 11:53:14
---

{% note info %} 學習 Kubernetes 與基本操作紀錄 {% endnote %}


<!--more-->

# Kubernetes 文章


- [学习 Kubernetes 基础知识](https://kubernetes.io/zh/docs/tutorials/kubernetes-basics/)
官方
- [[Day 6] 實際環境運行的 Kubernetes - Node & Architecture Overview](https://ithelp.ithome.com.tw/articles/10193248)
概觀 Kubernetes 的內部運作

- [Kubernetes 元件介紹與 minikube 安裝教學](https://blog.toright.com/posts/6513/kubernetes-%E5%9F%BA%E7%A4%8E%E5%85%83%E4%BB%B6%E4%BB%8B%E7%B4%B9%E8%88%87minikube%E5%AE%89%E8%A3%9D.html)
pod/Service/Deployment介紹

- [适用于 Docker 用户的 kubectl](https://kubernetes.io/zh/docs/reference/kubectl/docker-cli-to-kubectl/)
提供docker與kubectl指令對應參考

- [[Day 5] 在 Minikube 上跑起你的 Docker Containers - Pod & kubectl 常用指令](https://ithelp.ithome.com.tw/articles/10193232)
pod與yaml說明與如何與 Pod 中的 container 互動

- [Day 4 - 部署應用程式到 Kubernetes 叢集 - Part I - 手動建立 deployment 與 Service](https://ithelp.ithome.com.tw/articles/10202313)
建立deployment 與 Service/nodePort從本地開啟

- [Kubernetes & OpenShift Java Client](https://github.com/fabric8io/kubernetes-client)


- Kubernetes —學習好幫手minikube — 01
將K8s所需的Master/Worker node封裝在一個虛擬機器中
https://medium.com/@sniperbean/kubernetes-%E5%AD%B8%E7%BF%92%E5%A5%BD%E5%B9%AB%E6%89%8Bminikube-01-aedfaf8b00fe

# kubectl的簡單查看，新增，重開

kubectl的簡單查看，新增，重開

- kubectl get pod -A 

kubectl create 建立 後面可以直接加參數或是用yaml來建立

- 簡單建立deployment
啟動 minikube 之後，我們可以透過 kubectl run 在 minikube 上運行一個 Google 提供的 hello-minikube docker image，
```
$ kubectl create deployment first-deployment --image=katacoda/docker-http-server
deployment.apps/first-deployment created
$ kubectl get pods
NAME                               READY   STATUS    RESTARTS   AGE
first-deployment-8cbf74484-xgc4l   1/1     Running   0          25s
```

- 建立namespaces
```
>kubectl get namespaces
NAME              STATUS   AGE
default           Active   7m52s
kube-node-lease   Active   7m53s
kube-public       Active   7m53s
kube-system       Active   7m53s

 //Create a new Namespaces
D:\k8syaml>kubectl create namespace my
namespace/my created
```

- 建立deployment
https://kubernetes.io/zh/docs/concepts/workloads/controllers/deployment/
D:\k8syaml>kubectl create -f my-first-pod.yaml   編輯要部屬的程式
deployment.apps/my-pod created


- 查看所有pod
D:\k8syaml>kubectl get pod -A

- 看LOG
kubectl -n eda logs my-pod-5b788d95bc-kx76k

- 刪除
D:\k8syaml>kubectl delete deployment my-pod -n eda  先刪除
deployment.apps "my-pod" deleted

- 重開
D:\k8syaml>kubectl -n eda rollout restart deployment  nginx179   執行重開指令
deployment.apps/nginx179 restarted   

- 編輯一樣可以達到重開效果
kubectl edit deployment -n eda  nginx179
kubectl get pod -A
NAMESPACE     NAME                               READY   STATUS    RESTARTS   AGE
eda           nginx179-5ddfbfccb8-76qz8          1/1     Running   0          84s//啟動成功

# minikube 

Kubernetes —學習好幫手minikube — 01
將K8s所需的Master/Worker node封裝在一個虛擬機器中
https://medium.com/@sniperbean/kubernetes-%E5%AD%B8%E7%BF%92%E5%A5%BD%E5%B9%AB%E6%89%8Bminikube-01-aedfaf8b00fe
1.install kubuctl
你可以使用 Kubectl 命令行工具管理 Kubernetes 集群。 kubectl 在 $HOME/.kube 目录中查找一个名为 config 的配置文件。

2.Minikube 
>Minikube 是由 Google 發布的一個輕量級工具。讓開發者可以在本機上輕易架設一個 Kubernetes Cluster，快速上手 Kubernetes 的指令與環境。Minikube 會在本機上跑起一個 virtual machine，並且在這 VM 裡建立一個 signle-node Kubernetes Cluster，本身並不支援 HA (High availability)，也不推薦在實際應用上運行。

安裝:https://minikube.sigs.k8s.io/docs/start/

*開啟docker的k8s設定
docker desktop ->settings->

```
>kubectl get nodes
No resources found

- 啟動minikube start
>minikube start
* minikube v1.16.0 on Microsoft Windows 10 Enterprise 10.0.17763 Build 17763
* Using the docker driver based on existing profile
* Starting control plane node minikube in cluster minikube
* Restarting existing docker container for "minikube" ...
* Preparing Kubernetes v1.20.0 on Docker 20.10.0 ...
* Verifying Kubernetes components...
* Enabled addons: storage-provisioner, default-storageclass
* Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default
```

- 確認kubectl version
```
>kubectl version
Client Version: version.Info{Major:"1", Minor:"19", GitVersion:"v1.19.3", GitCommit:"1e11e4a2108024935ecfcb2912226cedeafd99df", GitTreeState:"clean", BuildDate:"2020-10-14T12:50:19Z", GoVersion:"go1.15.2", Compiler:"gc", Platform:"windows/amd64"}
Server Version: version.Info{Major:"1", Minor:"20", GitVersion:"v1.20.0", GitCommit:"af46c47ce925f4c4ad5cc8d1fca46c7b77d13b38", GitTreeState:"clean", BuildDate:"2020-12-08T17:51:19Z", GoVersion:"go1.15.5", Compiler:"gc", Platform:"linux/amd64"}
```
server version需要minikube有安裝才會出現
```
>kubectl get nodes
NAME       STATUS   ROLES                  AGE   VERSION
minikube   Ready    control-plane,master   3d    v1.20.0
```

PS C:\> minikube dashboard
Opening kubernetes dashboard in default browser...


啟動 minikube 之後，我們可以透過 kubectl run 在 minikube 上運行一個 Google 提供的 hello-minikube docker image，

$ kubectl create deployment first-deployment --image=katacoda/docker-http-server
deployment.apps/first-deployment created
$ kubectl get pods
NAME                               READY   STATUS    RESTARTS   AGE
first-deployment-8cbf74484-xgc4l   1/1     Running   0          25s


在 minikube 上透過 kubectl get

來自 <https://ithelp.ithome.com.tw/articles/10197186> 

D:\k8syaml>kubectl get namespaces
NAME              STATUS   AGE
default           Active   7m52s
kube-node-lease   Active   7m53s
kube-public       Active   7m53s
kube-system       Active   7m53s

Create a new Namespaces
D:\k8syaml>kubectl create namespace eda
namespace/eda created


建立deployment
https://kubernetes.io/zh/docs/concepts/workloads/controllers/deployment/
D:\k8syaml>kubectl create -f my-first-pod.yaml   編輯要部屬的程式
deployment.apps/my-pod created

D:\k8syaml>kubectl get pods
No resources found in default namespace.

D:\k8syaml>kubectl get pod -A
NAMESPACE     NAME                               READY   STATUS    RESTARTS   AGE
eda           my-pod-5b788d95bc-kx76k            0/1     Error     0          46s  建立不成功因為有相依
kube-system   coredns-74ff55c5b-wf484            1/1     Running   0          10m
kube-system   etcd-minikube                      1/1     Running   0          10m
kube-system   kube-apiserver-minikube            1/1     Running   0          10m
kube-system   kube-controller-manager-minikube   1/1     Running   0          10m
kube-system   kube-proxy-skl6r                   1/1     Running   0          10m
kube-system   kube-scheduler-minikube            1/1     Running   0          10m
kube-system   storage-provisioner                1/1     Running   0          10m

看LOG
kubectl -n eda logs my-pod-5b788d95bc-kx76k


D:\k8syaml>kubectl delete deployment my-pod -n eda  先刪除
deployment.apps "my-pod" deleted

D:\k8syaml>kubectl get pod -A
NAMESPACE     NAME                               READY   STATUS        RESTARTS   AGE
eda           my-pod-5b788d95bc-kx76k            0/1     Terminating   5          6m20s
kube-system   coredns-74ff55c5b-wf484            1/1     Running       0          16m
kube-system   etcd-minikube                      1/1     Running       0          16m
kube-system   kube-apiserver-minikube            1/1     Running       0          16m
kube-system   kube-controller-manager-minikube   1/1     Running       0          16m
kube-system   kube-proxy-skl6r                   1/1     Running       0          16m
kube-system   kube-scheduler-minikube            1/1     Running       0          16m
kube-system   storage-provisioner                1/1     Running       0          16m

D:\k8syaml>kubectl get pod -A
NAMESPACE     NAME                               READY   STATUS    RESTARTS   AGE
kube-system   coredns-74ff55c5b-wf484            1/1     Running   0          16m
kube-system   etcd-minikube                      1/1     Running   0          16m
kube-system   kube-apiserver-minikube            1/1     Running   0          16m
kube-system   kube-controller-manager-minikube   1/1     Running   0          16m
kube-system   kube-proxy-skl6r                   1/1     Running   0          16m
kube-system   kube-scheduler-minikube            1/1     Running   0          16m
kube-system   storage-provisioner                1/1     Running   0          16m

D:\k8syaml>kubectl create -f my-first-nginx179.yaml //重新建立一個
deployment.apps/nginx179 created

D:\k8syaml>kubectl get pod -A
NAMESPACE     NAME                               READY   STATUS    RESTARTS   AGE
eda           nginx179-75c6f6f5b8-bwzgm          1/1     Running   0          98s  //啟動成功
kube-system   coredns-74ff55c5b-wf484            1/1     Running   0          20m
kube-system   etcd-minikube                      1/1     Running   0          20m
kube-system   kube-apiserver-minikube            1/1     Running   0          20m
kube-system   kube-controller-manager-minikube   1/1     Running   0          20m
kube-system   kube-proxy-skl6r                   1/1     Running   0          20m
kube-system   kube-scheduler-minikube            1/1     Running   0          20m
kube-system   storage-provisioner                1/1     Running   0          20m

D:\k8syaml>kubectl -n eda rollout restart deployment  nginx179   執行重開指令
deployment.apps/nginx179 restarted   

編輯一樣可以達到重開效果
kubectl edit deployment -n eda  nginx179
kubectl get pod -A
NAMESPACE     NAME                               READY   STATUS    RESTARTS   AGE
eda           nginx179-5ddfbfccb8-76qz8          1/1     Running   0          84s//啟動成功


建立stateful
https://kubernetes.io/zh/docs/tutorials/stateful-application/basic-stateful-set/

D:\k8syaml>kubectl apply -f my-web.yaml
service/nginx created
statefulset.apps/web created
D:\k8syaml>kubectl get pods -A
NAMESPACE     NAME                               READY   STATUS    RESTARTS   AGE
default       web-0                              1/1     Running   0          39s
default       web-1                              1/1     Running   0          27s

D:\k8syaml>kubectl delete pod -l app=nginx
pod "web-0" deleted
pod "web-1" deleted

D:\k8syaml>kubectl apply -f my-web.yaml
service/nginx unchanged
statefulset.apps/web created

D:\k8syaml>kubectl edit statefulset -n eda  my-web
Edit cancelled, no changes made.


