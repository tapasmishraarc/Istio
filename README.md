# Istio

curl -L https://git.io/getLatestIstio | sh -

for i in install/kubernetes/helm/istio-init/files/crd*yaml; do kubectl apply -f $i; done

kubectl apply -f install/kubernetes/istio-demo.yaml


kubectl label namespace default istio-injection=enabled

kubectl apply -f ./samples/bookinfo/networking/bookinfo-gateway.yaml

kubectl apply -f ./samples/bookinfo/networking/destination-rule-all.yaml 

kubectl apply -f ./samples/bookinfo/networking/virtual-service-all-v1.yaml

export INGRESS_PORT=$(kubectl -n istio-system get service istio-ingressgateway -o jsonpath='{.spec.ports[?(@.name=="http2")].nodePort}')

kubectl apply -f ./samples/bookinfo/networking/virtual-service-reviews-test-v2.yaml

kubectl apply -f ./samples/bookinfo/networking/virtual-service-reviews-v2-v3.yaml

while true; do curl -s http://35.237.84.192//productpage > /dev/null && echo -n . && sleep 0.2; done

kubectl -n istio-system port-forward $(kubectl -n istio-system get pod -l app=grafana -o jsonpath='{.items[0].metadata.name}') 3000:3000 &



kubectl port-forward -n istio-system $(kubectl get pod -n istio-system -l app=jaeger -o jsonpath='{.items[0].metadata.name}') 16686:16686  &

kubectl create clusterrolebinding "cluster-admin-$(whoami)" --clusterrole=cluster-admin --user="$(gcloud config get-value core/account)"


kubectl apply -f "https://cloud.weave.works/k8s/scope.yaml?k8s-version=$(kubectl version | base64 | tr -d '\n')"

kubectl port-forward -n weave "$(kubectl get -n weave pod --selector=weave-scope-component=app -o jsonpath='{.items..metadata.name}')" 4040

