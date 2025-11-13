


```shell
for POD in $( kubectl get pods -n $NAMESPACE --no-headers -o custom-columns=":metadata.name");
do
echo "=== $POD ==="
  istioctl proxy-config secret "$POD" -n "$NAMESPACE" -o json \
    | jq -r '.dynamicActiveSecrets[].secret.tlsCertificate.certificateChain.inlineBytes' \
    | base64 -d \
    | openssl x509 -noout -text \
    | grep URI: | sed 's/ *URI://'
	
done
```

Script that dumps all spiffe certifcate fields of all PODs that have side-car proxies injected:

```shell
$ cat dump_spiffe.sh

#!/usr/bin/env bash

# Exit immediately on errors
set -e

# Check parameter
if [ -z "$1" ]; then
  echo "Usage: $0 <namespace>"
  exit 1
fi

NAMESPACE="$1"

echo "Listing SPIFFE IDs for all Istio-injected pods in namespace: $NAMESPACE"
echo

# Find all pods with sidecars in the namespace
PODS=$(kubectl get pod -n "$NAMESPACE" -l security.istio.io/tlsMode -o jsonpath='{.items[*].metadata.name}')

if [ -z "$PODS" ]; then
  echo "No Istio-injected pods found in namespace '$NAMESPACE'."
  exit 0
fi

# Loop over the pods and print their SPIFFE IDs
for POD in $PODS; do
  echo "=== $POD ==="

  istioctl proxy-config secret "$POD" -n "$NAMESPACE" -o json \
    | jq -r '.dynamicActiveSecrets[].secret.tlsCertificate.certificateChain.inlineBytes' \
    | base64 -d \
    | openssl x509 -noout -text \
    | grep URI: | sed 's/ *URI://'

  echo
done

```