# DDN

## Set up OpenShift Image Registry

Set up a PV/PVC binding for local storage on a node

Edit `imageregistry-storage.yaml` and set:
- `path: /mnt/disks/ssd1` with the actual path to the storage
- `example-node` with the name of the node (`oc get nodes`)

Size doesn't matter, there is no quota system

```bash
oc apply -f imageregistry-storage.yaml
```

## Build exa-client

Copy the exa-client tarball to `source/`

```bash
cd source
oc new-build -n openshift-kmm --binary --name exa-client
oc start-build -n openshift-kmm exa-client --from-dir . --follow
```

## KMM

Use this configmap for the build

```bash
oc apply -n openshift-kmm -f lustre-dockerfile-configmap.yaml
```

Build lnet module

```bash
oc apply -n openshift-kmm -f lnet-mod.yaml
```
