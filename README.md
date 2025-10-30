# Harbor Quickstart
Creating purely for quick testing of the Harbor registry in Kubernetes

## Installing Harbor

Create a network namespace called ```harbor```

Download the ```values.yaml``` file for your specific Harbor installation:
```
wget 
```
Now, install fresh using your adjusted, minimal ```values.yaml``` file.
```
helm install harbor harbor/harbor \
  --namespace harbor \
  -f values.yaml
```

```port-forward``` in a new terminal
```
kubectl port-forward svc/harbor-portal 8080:80 --namespace harbor
```

You can now access the Harbor app at ```http://localhost:8080``` in your web browser.

## Cleanup
Uninstall Harbor:
```
helm uninstall harbor -n harbor
```

The old database data is still saved in a Persistent Volume Claim (PVC). <br/>
You must delete this, or the new installation will just re-use the corrupted data.
```
kubectl delete pvc -n harbor --all
```
