# Mounting an Azure File Share as a network drive to a windows container
## tl;dr
Mount your network drive to ``C:`` instead of ``B:``

Today I needed to mount an Azure File Share to an exisiting Windows Server 2022 pod in Kubernetes. The PV and PVC were fine, I was using Access Key authentication as my Pod couldn't get its own identity and service account. The problem was that while technically the mount should have worked, it didn't. I got the following error message: 
```txt
Error: failed to create containerd task: failed to create shim task: hcs::CreateComputeSystem my-chart: The parameter is incorrect.: unknown
```

This was the snippet I used in the pod spec:
```yaml
volumeMounts:
  - name: pv-bibdata
    mountPath: "B:/webfadata"
```

That all seemed correct, but what I learned was that Windows containers for some reason don't (by default) expect any other drives than "C:\". The fix:
```yaml
volumeMounts:
  - name: pv-bibdata
    mountPath: "C:/webfadata"
```
Just mount the drive to "C:\" and you're done :-)
