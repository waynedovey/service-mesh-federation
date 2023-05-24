# service-mesh-federation

Create two Clusters -> ACM 

Example sydney-cluster and singapore-cluster

Apply the Policy to the Hub Cluster

```
oc apply -f sydney-cluster-policy.yaml
```

```
oc apply -f singapore-cluster-policy.yaml
```

Checkout https://github.com/maistra/istio.git

```
git clone https://github.com/maistra/istio.git
```

```
cd ~/istio/samples/federation/base/
```
```
export MESH1_KUBECONFIG=/root/istio/samples/federation/base/singapore-cluster-kubeconfig.yaml
```
```
export MESH2_KUBECONFIG=/root/istio/samples/federation/base/sydney-cluster-kubeconfig.yaml
```

Install the Bookinfo Federation example
```
./install.sh
```

Review the Bookinfo URL 

```
export CLUSTER_DOMAIN=sandbox897.opentlc.com
```
```
http://istio-ingressgateway-mesh2-system.apps.sydney-cluster.${CLUSTER_DOMAIN}/productpage
```
Send load to the Bookinfo URL
```
ab -c 100 -n 10000 http://istio-ingressgateway-mesh2-system.apps.sydney-cluster.${CLUSTER_DOMAIN}/productpage
```

Review the Kiali service 

```
https://kiali-mesh2-system.apps.sydney-cluster.${CLUSTER_DOMAIN}/console/overview?duration=3600&refresh=60000
```
