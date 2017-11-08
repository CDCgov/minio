Minio Container for OpenShift 3
===============================

Version of a popular Minio Docker image (docker pull spec: minio/minio)
that will run on OpenShift 3 with the default Security Context Constraint (SCC)
of restricted.

The latest stable minio docker image does **not** run under the **restricted** SCC as it is, due to
its use of /${HOME}/.minio for minio's configuration file directory. Since ${HOME} is set to /, this results
in permission errors when using an arbitrary non-root uid. Despite this problem, we **are** able to use the
unmodified upstream image as long as our templates pass an alternative location for that configuration file
directory via the "--config-dir" argument to minio, as our templates do in this repository. Consequently,
no customization of the image is required at this time.

# Importing Docker image into OpenShift
There is a YAML file in the openshift directory (minio-imagestream.yml) which will
import the minio image(s) into the internal registry of an OpenShift
cluster.

