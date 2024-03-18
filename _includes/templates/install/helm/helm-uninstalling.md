To delete installed chart please execute the following
```shell
helm delete my-thingsboard-cluster -n namespace
```

The command removes all the Thingsboard components associated with the chart and deletes the release.

If you want to completely delete everything, after chart deletion you need to delete volumes.

```shell
kubectl delete pvc -l release=my-thingsboard-cluster
```
