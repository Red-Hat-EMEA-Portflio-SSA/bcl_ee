# bcl_ee
# The execution environment needed to set up the BCL demo in the CIC
# here are the steps to
 podman login quay.io
 podman login registry.redhat.io
 ansible-builder build -v 3 -t bcl-ov2:1 -f execution-environment.yml


# and pushed to quay.io
 podman push bcl-ov2:1 quay.io/mschreie/bcl-ov2:1

# and pushed to private automation hub
 podman login --tls-verify=false aap-privhub.bcl.redhat.hpecic.com
Username: admin
Password:
Login Succeeded!
 podman push --tls-verify=false bcl-ov:3 aap-privhub.bcl.redhat.hpecic.com/bcl-ov:latest
