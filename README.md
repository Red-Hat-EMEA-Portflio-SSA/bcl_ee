# bcl_ee
# The execution environment needed to set up the BCL demo in the CIC
# here are the steps to
 ```
 podman login quay.io
 ```
 ```
 podman login registry.redhat.io
 ```
 ```
 ansible-builder build -v 3 -t bcl-ov:4 -f execution-environment.yml
 ```


# and pushed to quay.io
 ```
 podman push bcl-ov:4 quay.io/mschreie/bcl-ov:4
 ```

# and pushed to private automation hub
 ```
 podman login --tls-verify=false aap-privhub.bcl.redhat.hpecic.com
 Username: admin
```
```
 podman push --tls-verify=false bcl-ov:4 aap-privhub.bcl.redhat.hpecic.com/bcl-ov:latest
 ```

# Version 14 and above > Including vSAN management 

For using the modules that manage vSAN with the community.vmware collection you need to include the vSAN Management python SDK. This SDK is provided and managed by VMware in a way that cannot just be included in the requirements.txt file. Here I explain how to include it in your execution environment to build version 14 of bcl_ee and above.

First thing you need to do is dowload the "vsan-sdk-python.zip" [from VMware site](https://developer.vmware.com/web/sdk/7.0%20U2/vsan-python) and place the file in the directory of this repo: /your-path/bcl_ee/vsan-sdk-python.zip

Once you have it there you need to execute ansible-builder with the schema version 3 file:

```
ansible-builder build -v 3 -t bcl-ov:14 -f ee-schema-v3.yml
```

Then push it the same way we did before:
```
podman push bcl-ov:14 quay.io/mschreie/bcl-ov:14
```