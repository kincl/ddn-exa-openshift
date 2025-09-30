# DDN

## Build exa-client

cd source

(copy exa-client tarball)

oc new-build --binary --name exa-client
oc start-build exa-client --from-dir . --follow

## KMM
