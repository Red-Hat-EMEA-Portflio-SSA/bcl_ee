# bcl_ee
# The execution environment needed to set up the BCL demo in the CIC
# here are the steps to
 podman login quay.io
 podman login registry.redhat.io
 ansible-builder build -t bcl-ov:4
