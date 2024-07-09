# Splunk Standalone Instance with Splunk Operator 

A Kubernetes cluster administrator can install and start the Splunk Operator for cluster-wide by running:

                 kubectl apply -f splunk-operator.yaml --server-side  --force-conflicts

Deploying a splunk standalone instance through kuberentes 

                    kubectl apply -n splunk-operator -f splunk-enterprise.yaml

The enterprise.splunk.com/delete-pvc finalizer is optional, and tells the Splunk Operator to remove any Kubernetes Persistent Volumes associated with the instance if you delete the custom resource(CR).
