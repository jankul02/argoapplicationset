# install kubernetes

curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube_latest_amd64.deb
sudo dpkg -i minikube_latest_amd64.deb

kubectl config get-contexts
CURRENT   NAME                    CLUSTER           AUTHINFO                                    NAMESPACE
*         minikube                minikube          minikube                                    default
          test121-cluster         test121-cluster   clusterUser_test121-kaas_test121-cluster    
          test121-cluster-admin   test121-cluster   clusterAdmin_test121-kaas_test121-cluster   

kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/master/manifests/install.yaml

brew install argocd


kubectl port-forward svc/argocd-server -n argocd 8080:443

kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
# browser  login with localhost:8080 
argocd app create guestbook --repo https://github.com/argoproj/argocd-example-apps.git --path guestbook --dest-server https://kubernetes.default.svc --dest-namespace default


# additionally
argocd login localhost:8080


kubectl apply -n argocd -f git-generator-files-discovery/git-generator-files.yaml 

kubectl delete -n argocd -f git-generator-files-discovery/git-generator-files.yaml 


 kubectl config get-contexts
CURRENT   NAME                    CLUSTER           AUTHINFO                                    NAMESPACE
*         minikube                minikube          minikube                                    default
          test121-cluster         test121-cluster   clusterUser_test121-kaas_test121-cluster    
          test121-cluster-admin   test121-cluster   clusterAdmin_test121-kaas_test121-cluster 


kubectl config use-context test121-cluster-admin


kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/master/manifests/install.yaml

kubectl port-forward svc/argocd-server -n argocd 8080:443

kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo

 kubectl apply -n argocd -f https://raw.githubusercontent.com/jankul02/argoapplicationset/master/git-generator-files-discovery/git-generator-files.yaml