

Check which backends the proxy has configured:

```shell

istioctl proxy-config clusters <your-ingressgateway-pod> -n istio-system

```


Example:

```shell
$ istioctl proxy-config clusters gateway-main-istio-79b9855848-2rmsv -n istio-system
SERVICE FQDN                                                   PORT      SUBSET     DIRECTION     TYPE       DESTINATION RULE
BlackHoleCluster                                               -         -          -             STATIC
agent                                                          -         -          -             STATIC
details-v1.sample.svc.cluster.local                            9080      -          outbound      EDS
details.sample.svc.cluster.local                               9080      -          outbound      EDS
gateway-main-istio.istio-system.svc.cluster.local              443       -          outbound      EDS
gateway-main-istio.istio-system.svc.cluster.local              15021     -          outbound      EDS
grafana.istio-system.svc.cluster.local                         3000      -          outbound      EDS
httpbin.default.svc.cluster.local                              8000      -          outbound      EDS
istiod-revision-tag-default.istio-system.svc.cluster.local     443       -          outbound      EDS
istiod-revision-tag-default.istio-system.svc.cluster.local     15010     -          outbound      EDS
istiod-revision-tag-default.istio-system.svc.cluster.local     15012     -          outbound      EDS
istiod-revision-tag-default.istio-system.svc.cluster.local     15014     -          outbound      EDS
istiod.istio-system.svc.cluster.local                          443       -          outbound      EDS
istiod.istio-system.svc.cluster.local                          15010     -          outbound      EDS
istiod.istio-system.svc.cluster.local                          15012     -          outbound      EDS
istiod.istio-system.svc.cluster.local                          15014     -          outbound      EDS
jaeger-collector.istio-system.svc.cluster.local                4317      -          outbound      EDS
jaeger-collector.istio-system.svc.cluster.local                4318      -          outbound      EDS
jaeger-collector.istio-system.svc.cluster.local                9411      -          outbound      EDS
jaeger-collector.istio-system.svc.cluster.local                14250     -          outbound      EDS
jaeger-collector.istio-system.svc.cluster.local                14268     -          outbound      EDS
kiali.istio-system.svc.cluster.local                           9090      -          outbound      EDS
kiali.istio-system.svc.cluster.local                           20001     -          outbound      EDS
kube-dns.kube-system.svc.cluster.local                         53        -          outbound      EDS
kube-dns.kube-system.svc.cluster.local                         9153      -          outbound      EDS
kubernetes.default.svc.cluster.local                           443       -          outbound      EDS
loki-headless.istio-system.svc.cluster.local                   3100      -          outbound      EDS
loki-memberlist.istio-system.svc.cluster.local                 7946      -          outbound      EDS
loki.istio-system.svc.cluster.local                            3100      -          outbound      EDS
loki.istio-system.svc.cluster.local                            9095      -          outbound      EDS
metallb-webhook-service.metallb-system.svc.cluster.local       443       -          outbound      EDS
productpage-v1.sample.svc.cluster.local                        9080      -          outbound      EDS
productpage.sample.svc.cluster.local                           9080      -          outbound      EDS
prometheus.istio-system.svc.cluster.local                      9090      -          outbound      EDS
prometheus_stats                                               -         -          -             STATIC
ratings-v1.sample.svc.cluster.local                            9080      -          outbound      EDS
ratings.sample.svc.cluster.local                               9080      -          outbound      EDS
reviews-v1.sample.svc.cluster.local                            9080      -          outbound      EDS
reviews-v2.sample.svc.cluster.local                            9080      -          outbound      EDS
reviews-v3.sample.svc.cluster.local                            9080      -          outbound      EDS
reviews.sample.svc.cluster.local                               9080      -          outbound      EDS
sds-grpc                                                       -         -          -             STATIC
tcp-echo-service.echo.svc.cluster.local                        2701      -          outbound      EDS
tracing.istio-system.svc.cluster.local                         80        -          outbound      EDS
tracing.istio-system.svc.cluster.local                         16685     -          outbound      EDS
xds-grpc                                                       -         -          -             STATIC
zipkin.istio-system.svc.cluster.local                          9411      -          outbound      EDS
```

Istio uses it's `VirutalServices` to get the corresponding K8S services. Based on these services Istio retrieves the corresponding POD endpoints from the API-server and configures it to the sidecar-proxy.

#istio 
#Routiung