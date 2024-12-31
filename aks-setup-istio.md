1. increase VCPU quota to 8
2. create AKS with system nodepool with one node
3. select enable istio service mesh option
4. select Internal ingress gateway and External ingress gateway check boxes

## After AKS creation
1. disable "Internal ingress gateway"
2. az aks get-credentials --resource-group aks-learn --name istio-learn --overwrite-existing
3. kubectl get po -A
4. kubectl get svc -A
5. follow the steps in this https://istio.io/latest/docs/setup/getting-started/#bookinfo
6. kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.24/samples/bookinfo/platform/kube/bookinfo.yaml
7.  kubectl get services
   
Events:
  Type     Reason            Age   From               Message
  ----     ------            ----  ----               -------
  Warning  FailedScheduling  89s   default-scheduler  0/1 nodes are available: 1 node(s) had untolerated taint {CriticalAddonsOnly: true}. preemption: 0/1 nodes are available: 1 Preemption is not helpful for scheduling.

9. create a new use node pool
10. kubectl exec "$(kubectl get pod -l app=ratings -o jsonpath='{.items[0].metadata.name}')" -c ratings -- curl -sS productpage:9080/productpage | grep -o "<title>.*</title>"
<title>Simple Bookstore App</title>

11.  kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.24/samples/bookinfo/gateway-api/bookinfo-gateway.yaml
  resource mapping not found for name: "bookinfo-gateway" namespace: "" from "https://raw.githubusercontent.com/istio/istio/release-1.24/samples/bookinfo/gateway-api/bookinfo-gateway.yaml": no matches for kind "Gateway" in version "gateway.networking.k8s.io/v1"
ensure CRDs are installed first
resource mapping not found for name: "bookinfo" namespace: "" from "https://raw.githubusercontent.com/istio/istio/release-1.24/samples/bookinfo/gateway-api/bookinfo-gateway.yaml": no matches for kind "HTTPRoute" in version "gateway.networking.k8s.io/v1"

12. enable "Internal ingress gateway"
13. kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.24/samples/bookinfo/gateway-api/bookinfo-gateway.yaml -n default
resource mapping not found for name: "bookinfo-gateway" namespace: "" from "https://raw.githubusercontent.com/istio/istio/release-1.24/samples/bookinfo/gateway-api/bookinfo-gateway.yaml": no matches for kind "Gateway" in version "gateway.networking.k8s.io/v1"
ensure CRDs are installed first
resource mapping not found for name: "bookinfo" namespace: "" from "https://raw.githubusercontent.com/istio/istio/release-1.24/samples/bookinfo/gateway-api/bookinfo-gateway.yaml": no matches for kind "HTTPRoute" in version "gateway.networking.k8s.io/v1"
ensure CRDs are installed first

14. kubectl get crd gateways.gateway.networking.k8s.io &> /dev/null || \
{ kubectl kustomize "github.com/kubernetes-sigs/gateway-api/config/crd?ref=v1.2.0" | kubectl apply -f -; }

15. kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.24/samples/bookinfo/gateway-api/bookinfo-gateway.yaml

gateway.gateway.networking.k8s.io/bookinfo-gateway created
httproute.gateway.networking.k8s.io/bookinfo created

16. kubectl annotate gateway bookinfo-gateway networking.istio.io/service-type=ClusterIP --namespace=default

gateway.gateway.networking.k8s.io/bookinfo-gateway annotated
17. kubectl get gateway

NAME               CLASS   ADDRESS   PROGRAMMED   AGE
bookinfo-gateway   istio             False        4m25s

18. kubectl port-forward svc/bookinfo-gateway-istio 8080:80

Error from server (NotFound): services "bookinfo-gateway-istio" not found

19. kubectl delete -f https://raw.githubusercontent.com/istio/istio/release-1.24/samples/bookinfo/gateway-api/bookinfo-gateway.yaml

gateway.gateway.networking.k8s.io "bookinfo-gateway" deleted
httproute.gateway.networking.k8s.io "bookinfo" deleted

20. kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.24/samples/bookinfo/gateway-api/bookinfo-gateway.yaml

gateway.gateway.networking.k8s.io/bookinfo-gateway created
httproute.gateway.networking.k8s.io/bookinfo created

21. kubectl annotate gateway bookinfo-gateway networking.istio.io/service-type=ClusterIP --namespace=default

gateway.gateway.networking.k8s.io/bookinfo-gateway annotated

22. ubectl get gateway

NAME               CLASS   ADDRESS   PROGRAMMED   AGE

bookinfo-gateway   istio             False        55s

23. kubectl get gateway

NAME               CLASS   ADDRESS   PROGRAMMED   AGE

bookinfo-gateway   istio             False        3m5s

24. kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.22/samples/bookinfo/gateway-api/bookinfo-gateway.yaml

gateway.gateway.networking.k8s.io/bookinfo-gateway configured<br>
httproute.gateway.networking.k8s.io/bookinfo configured
