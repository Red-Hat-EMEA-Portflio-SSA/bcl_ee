# bcl_ee
# The execution environment needed to set up the BCL demo in the CIC
# here are the steps to

Set the version in a variable to allow cut and past in the following
 ```
 export eev=15
 ```
Login to quay and RH registry to download things needed
 ```
 podman login quay.io
 ```
 ```
 podman login registry.redhat.io
 ```
Build a new execution environment
 ```
 ansible-builder build -v 3 -t bcl-ov:${eev} -f execution-environment.yml --prune-images
 ```

# Version 14 and above > Including vSAN management 

For using the modules that manage vSAN with the community.vmware collection you nepodman push bcl-ov:4 quay.io/mschreie/bcl-ov:ed to include the vSAN Management python SDK. This SDK is provided and managed by VMware in a way that cannot just be included in the requirements.txt file. Here I explain how to include it in your execution environment to build version 14 of bcl_ee and above.

First thing you need to do is dowload the "vsan-sdk-python.zip" [from VMware site](https://developer.vmware.com/web/sdk/7.0%20U2/vsan-python) and place the file in the directory of this repo: /your-path/bcl_ee/vsan-sdk-python.zip

Once you have it there you need to execute ansible-builder with the schema version 3 file:

```
ansible-builder build -v 3 -t bcl-ov:${eev} -f ee-schema-v3.yml --prune-images
```

Then follow the next steps (pushing it everywhere needed)

# and push to quay.io
 ```
 podman push bcl-ov:${eev} quay.io/mschreie/bcl-ov:${eev}
 podman push bcl-ov:${eev} quay.io/mschreie/bcl-ov:latest
 ```

# and push to private automation hub
 ```
 podman login --tls-verify=false aap-privhub.bcl.redhat.hpecic.com
 Username: admin
```
```
 podman push --tls-verify=false bcl-ov:${eev} aap-privhub.bcl.redhat.hpecic.com/bcl-ov:${eev}
 podman push --tls-verify=false bcl-ov:${eev} aap-privhub.bcl.redhat.hpecic.com/bcl-ov:latest
 ```
