# elastic-metricbeat-issue
We have deployed the metricbeat on our kubernetes cluster and noticing the below issue. The metrics are being pushed to elastic search without any issues.

```bash
2020-07-01T14:05:25.421Z     INFO    module/wrapper.go:259   Error fetching data for metricset kubernetes.apiserver: error getting metrics: unexpected status code 403 from server
```

This can be fixed by adding the below to the ClusterRole. It is now working without any issues.

```yaml
rules:
  - nonResourceURLs:
      - /metrics
    verbs:
      - get
```

We also need to have the kube-state-metrics up and running for the metricbeat to fetch all the metrics from the Kubernetes cluster.