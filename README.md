[![Apache Sling](https://sling.apache.org/res/logos/sling.png)](https://sling.apache.org)

&#32;[![Build Status](https://ci-builds.apache.org/job/Sling/job/modules/job/sling-org-apache-sling-commons-metrics-prometheus/job/master/badge/icon)](https://ci-builds.apache.org/job/Sling/job/modules/job/sling-org-apache-sling-commons-metrics-prometheus/job/master/)&#32;[![Test Status](https://img.shields.io/jenkins/tests.svg?jobUrl=https://ci-builds.apache.org/job/Sling/job/modules/job/sling-org-apache-sling-commons-metrics-prometheus/job/master/)](https://ci-builds.apache.org/job/Sling/job/modules/job/sling-org-apache-sling-commons-metrics-prometheus/job/master/test/?width=800&height=600)&#32;[![Coverage](https://sonarcloud.io/api/project_badges/measure?project=apache_sling-org-apache-sling-commons-metrics-prometheus&metric=coverage)](https://sonarcloud.io/dashboard?id=apache_sling-org-apache-sling-commons-metrics-prometheus)&#32;[![Sonarcloud Status](https://sonarcloud.io/api/project_badges/measure?project=apache_sling-org-apache-sling-commons-metrics-prometheus&metric=alert_status)](https://sonarcloud.io/dashboard?id=apache_sling-org-apache-sling-commons-metrics-prometheus)&#32;[![Maven Central](https://maven-badges.herokuapp.com/maven-central/org.apache.sling/org.apache.sling.commons.metrics.prometheus/badge.svg)](https://search.maven.org/#search%7Cga%7C1%7Cg%3A%22org.apache.sling%22%20a%3A%22org.apache.sling.commons.metrics.prometheus%22) [![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://www.apache.org/licenses/LICENSE-2.0)

# Apache Sling Commons Prometheus Metrics Exporter

This module is part of the [Apache Sling](https://sling.apache.org) project.

This bundle exposes the collected metrics under the `/metrics` path and provides the following features:

- exports JVM metrics by default
- supports multiple `MetricRegistry` instances

## Deployment

The bundle is compatible with [prometheus/client-java](https://github.com/prometheus/client_java/)
versions up to 0.10.0. Version 0.11.0 introduced a mandatory dependency on opentelemetry-api,
which is not a valid OSGi bundle. This was rectified in version 0.16.0, but unfortunately
versions >= 0.15.0 depend on version 4.0 of Dropwizard metrics, which is not supported by the current org.apache.sling.commons.metrics.bundle .

A recommended feature model file for deploying this bundle and additional dependencies is

```json
  "bundles": [
    {
        "id": "io.prometheus/simpleclient/0.10.0",
        "start-order": 20
    },
    {
        "id": "io.prometheus/simpleclient_common/0.10.0",
        "start-order": 20
    },
    {
        "id": "io.prometheus/simpleclient_servlet/0.10.0",
        "start-order": 20
    },
    {
        "id": "io.prometheus/simpleclient_dropwizard/0.10.0",
        "start-order": 20
    },
    {
        "id": "io.prometheus/simpleclient_hotspot/0.10.0",
        "start-order": 20
    },
    {
        "id": "org.apache.sling/org.apache.sling.commons.metrics.prometheus/1.0-SNAPSHOT",
        "start-order": 20
    }
  ]
```
