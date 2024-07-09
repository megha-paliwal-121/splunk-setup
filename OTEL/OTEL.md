# How to install

In order to install Splunk OpenTelemetry Collector in a Kubernetes cluster, at least one of the destinations (splunkPlatform or splunkObservability) has to be configured.

For Splunk Enterprise/Cloud the following parameters are required:
1. splunkPlatform.endpoint: URL to a Splunk instance, e.g. "http://localhost:8088/services/collector"
2. splunkPlatform.token: Splunk HTTP Event Collector token
   
For Splunk Observability Cloud the following parameters are required:
1. splunkObservability.realm: Splunk realm to send telemetry data to.
2. splunkObservability.accessToken: Your Splunk Observability org access token.
   
The following parameter is required or optional depending on the Kubernetes distribution:
1. clusterName: arbitrary value that identifies your Kubernetes cluster. The value will be associated with every trace, metric and log as "k8s.cluster.name" attribute.
   
Required: For all other distributions.

Run the following commands, replacing the parameters above with their appropriate values.
1. Add Helm repo

                 helm repo add splunk-otel-collector-chart https://signalfx.github.io/splunk-otel-collector-chart
                 
a. Sending data to Splunk Observability Cloud

      helm install my-splunk-otel-collector --set="splunkObservability.realm=us0,splunkObservability.accessToken=xxxxxx,clusterName=my-cluster" splunk-otel-collector-chart/splunk-otel-collector 

b. Sending data to Splunk Enterprise or Splunk Cloud

      helm install my-splunk-otel-collector --set="splunkPlatform.endpoint=https://127.0.0.1:8088/services/collector,splunkPlatform.token=xxxxxx,splunkPlatform.metricsIndex=k8s-metrics,splunkPlatform.index=main,clusterName=my-cluster" splunk-otel-collector-chart/splunk-otel-collector

c. Sending data to both Splunk Observability Cloud and Splunk Enterprise or Splunk Cloud

      helm install my-splunk-otel-collector --set="splunkPlatform.endpoint=https://127.0.0.1:8088/services/collector,splunkPlatform.token=xxxxxx,splunkPlatform.metricsIndex=k8s-metrics,splunkPlatform.index=main,splunkObservability.realm=us0,splunkObservability.accessToken=xxxxxx,clusterName=my-cluster" splunk-otel-collector-chart/splunk-otel-collector

d. You can specify a namespace to deploy the chart to with the -n argument. Here is an example showing how to deploy in the otel namespace:

      helm -n otel install my-splunk-otel-collector -f values.yaml splunk-otel-collector-chart/splunk-otel-collector
      
e. Instead of setting helm values as arguments a YAML file can be provided:

      helm install my-splunk-otel-collector --values my_values.yaml splunk-otel-collector-chart/splunk-otel-collector
