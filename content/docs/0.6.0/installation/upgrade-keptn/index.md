---
title: Upgrade Keptn
description: How to upgrade Keptn.
weight: 20
keywords: upgrade
---

## Upgrade from 0.6.1 to 0.6.2

* To download and install the Keptn CLI for version 0.6.2, please refer to the [Install Keptn CLI section](../setup-keptn/#install-keptn-cli).

* To upgrade your Keptn installation from 0.6.1 to 0.6.2, you can deploy a *Kubernetes Job* that will take care of updating all components to the 0.6.2 release. Please [verify that you are connected to the correct Kubernetes cluster](../../reference/troubleshooting/#verify-kubernetes-context-with-keptn-installation)
before deploying the upgrading job with the next command:

```console
kubectl -n default delete job upgrader
kubectl apply -f https://raw.githubusercontent.com/keptn/keptn/release-0.6.2/upgrader/upgrade-061-062/upgrade-job.yaml
```

* To check the status of the update job, please execute:

```console
kubectl -n default get job
```
```
NAME                COMPLETIONS   DURATION   AGE
upgrader            1/1           17s        20h
```

When the job is completed, your Keptn version has been updated to 0.6.2.

<details><summary>*Verifying that the upgrade worked*</summary>

To verify that the upgrade process worked, please check the images and their tags using `kubectl` as described below. 

**Before the upgrade**:

```console
kubectl -n keptn get deployments -owide
```


```console
NAME                                                      READY   UP-TO-DATE   AVAILABLE   AGE     CONTAINERS               IMAGES                                  SELECTOR
api                                                       1/1     1            1           4h39m   api                      keptn/api:0.6.1                         run=api
bridge                                                    1/1     1            1           4h39m   bridge                   keptn/bridge2:0.6.1                     run=bridge
configuration-service                                     1/1     1            1           4h39m   configuration-service    keptn/configuration-service:0.6.1       run=configuration-service
eventbroker-go                                            1/1     1            1           4h39m   eventbroker-go           keptn/eventbroker-go:0.6.1              run=eventbroker-go
gatekeeper-service                                        1/1     1            1           4h39m   gatekeeper-service       keptn/gatekeeper-service:0.6.1          run=gatekeeper-service
gatekeeper-service-evaluation-done-distributor            1/1     1            1           4h39m   distributor              keptn/distributor:0.6.1                 run=distributor
helm-service                                              1/1     1            1           4h39m   helm-service             keptn/helm-service:0.6.1                run=helm-service
helm-service-configuration-change-distributor             1/1     1            1           4h39m   distributor              keptn/distributor:0.6.1                 run=distributor
helm-service-service-create-distributor                   1/1     1            1           4h39m   distributor              keptn/distributor:0.6.1                 run=distributor
jmeter-service                                            1/1     1            1           4h39m   jmeter-service           keptn/jmeter-service:0.6.1              run=jmeter-service
jmeter-service-deployment-distributor                     1/1     1            1           4h39m   distributor              keptn/distributor:0.6.1                 run=distributor
lighthouse-service                                        1/1     1            1           4h39m   lighthouse-service       keptn/lighthouse-service:0.6.1          run=lighthouse-service
lighthouse-service-distributor                            1/1     1            1           72s     distributor              keptn/distributor:0.6.1                 run=distributor
nats-operator                                             1/1     1            1           4h40m   nats-operator            connecteverything/nats-operator:0.6.0   name=nats-operator
prometheus-service                                        1/1     1            1           41m     prometheus-service       keptn/prometheus-service:0.3.1          run=prometheus-service
prometheus-service-monitoring-configure-distributor       1/1     1            1           41m     distributor              keptn/distributor:0.5.0                 run=distributor
prometheus-sli-service                                    1/1     1            1           38m     prometheus-sli-service   keptn/prometheus-sli-service:0.2.1      run=prometheus-sli-service
prometheus-sli-service-monitoring-configure-distributor   1/1     1            1           38m     distributor              keptn/distributor:latest                run=distributor
remediation-service                                       1/1     1            1           4h39m   remediation-service      keptn/remediation-service:0.6.1         run=remediation-service
remediation-service-problem-distributor                   1/1     1            1           4h39m   distributor              keptn/distributor:0.6.1                 run=distributor
shipyard-service                                          1/1     1            1           4h39m   shipyard-service         keptn/shipyard-service:0.6.1            run=shipyard-service
shipyard-service-create-project-distributor               1/1     1            1           4h39m   distributor              keptn/distributor:0.6.1                 run=distributor
shipyard-service-delete-project-distributor               1/1     1            1           4h39m   distributor              keptn/distributor:0.6.1                 run=distributor
wait-service                                              1/1     1            1           4h39m   wait-service             keptn/wait-service:0.6.1                run=wait-service
wait-service-deployment-distributor                       1/1     1            1           4h39m   distributor              keptn/distributor:0.6.1                 run=distributor

```

```console
kubectl -n keptn-datastore get deployments -owide
```

```console
NAME                            READY   UP-TO-DATE   AVAILABLE   AGE     CONTAINERS          IMAGES                          SELECTOR
mongodb                         1/1     1            1           2m41s   mongodb             centos/mongodb-36-centos7:1     name=mongodb
mongodb-datastore               1/1     1            1           4h40m   mongodb-datastore   keptn/mongodb-datastore:0.6.1   run=mongodb-datastore
mongodb-datastore-distributor   1/1     1            1           4h40m   distributor         keptn/distributor:0.6.1         run=distributor
```

**After the upgrade**

```console
kubectl -n keptn get deployments -owide
```

**Full version of Keptn:**

```console
NAME                                             READY   UP-TO-DATE   AVAILABLE   AGE     CONTAINERS              IMAGES                                  SELECTOR
api-gateway-nginx                                1/1     1            1           3m6s    api-gateway-nginx       nginx:1.17.9                            run=api-gateway-nginx
api-service                                      1/1     1            1           3m6s    api-service             keptn/api:0.6.2                         run=api-service
bridge                                           1/1     1            1           9m38s   bridge                  keptn/bridge2:0.6.2                     run=bridge
configuration-service                            1/1     1            1           9m37s   configuration-service   keptn/configuration-service:0.6.2       run=configuration-service
eventbroker-go                                   1/1     1            1           9m38s   eventbroker-go          keptn/eventbroker-go:0.6.2              run=eventbroker-go
gatekeeper-service                               1/1     1            1           9m12s   gatekeeper-service      keptn/gatekeeper-service:0.6.2          run=gatekeeper-service
gatekeeper-service-evaluation-done-distributor   1/1     1            1           9m12s   distributor             keptn/distributor:0.6.2                 run=distributor
helm-service                                     1/1     1            1           9m38s   helm-service            keptn/helm-service:0.6.2                run=helm-service
helm-service-configuration-change-distributor    1/1     1            1           9m12s   distributor             keptn/distributor:0.6.2                 run=distributor
helm-service-service-create-distributor          1/1     1            1           9m37s   distributor             keptn/distributor:0.6.2                 run=distributor
jmeter-service                                   1/1     1            1           9m12s   jmeter-service          keptn/jmeter-service:0.6.2              run=jmeter-service
jmeter-service-deployment-distributor            1/1     1            1           9m11s   distributor             keptn/distributor:0.6.2                 run=distributor
lighthouse-service                               1/1     1            1           9m11s   lighthouse-service      keptn/lighthouse-service:0.6.2          run=lighthouse-service
lighthouse-service-distributor                   1/1     1            1           9m11s   distributor             keptn/distributor:0.6.2                 run=distributor
nats-operator                                    1/1     1            1           10m     nats-operator           connecteverything/nats-operator:0.6.0   name=nats-operator
remediation-service                              1/1     1            1           9m10s   remediation-service     keptn/remediation-service:0.6.2         run=remediation-service
remediation-service-problem-distributor          1/1     1            1           9m10s   distributor             keptn/distributor:0.6.2                 run=distributor
shipyard-service                                 1/1     1            1           9m37s   shipyard-service        keptn/shipyard-service:0.6.2            run=shipyard-service
shipyard-service-create-project-distributor      1/1     1            1           9m37s   distributor             keptn/distributor:0.6.2                 run=distributor
shipyard-service-delete-project-distributor      1/1     1            1           9m37s   distributor             keptn/distributor:0.6.2                 run=distributor
wait-service                                     1/1     1            1           9m10s   wait-service            keptn/wait-service:0.6.2                run=wait-service
wait-service-deployment-distributor              1/1     1            1           9m10s   distributor             keptn/distributor:0.6.2                 run=distributor
```

**Quality Gates only version of Keptn:**

```console
NAME                                          READY   UP-TO-DATE   AVAILABLE   AGE   CONTAINERS              IMAGES                                  SELECTOR
api-gateway-nginx                             1/1     1            1           23h   api-gateway-nginx       nginx:1.17.9                            run=api-gateway-nginx
api-service                                   1/1     1            1           23h   api-service             keptn/api:0.6.2                         run=api-service
bridge                                        1/1     1            1           23h   bridge                  keptn/bridge2:0.6.2                     run=bridge
configuration-service                         1/1     1            1           23h   configuration-service   keptn/configuration-service:0.6.2       run=configuration-service
eventbroker-go                                1/1     1            1           23h   eventbroker-go          keptn/eventbroker-go:0.6.2              run=eventbroker-go
helm-service                                  1/1     1            1           23h   helm-service            keptn/helm-service:0.6.2                run=helm-service
helm-service-service-create-distributor       1/1     1            1           23h   distributor             keptn/distributor:0.6.2                 run=distributor
lighthouse-service                            1/1     1            1           23h   lighthouse-service      keptn/lighthouse-service:0.6.2          run=lighthouse-service
lighthouse-service-distributor                1/1     1            1           23h   distributor             keptn/distributor:0.6.2                 run=distributor
nats-operator                                 1/1     1            1           23h   nats-operator           connecteverything/nats-operator:0.6.0   name=nats-operator
shipyard-service                              1/1     1            1           23h   shipyard-service        keptn/shipyard-service:0.6.2            run=shipyard-service
shipyard-service-create-project-distributor   1/1     1            1           23h   distributor             keptn/distributor:0.6.2                 run=distributor
shipyard-service-delete-project-distributor   1/1     1            1           23h   distributor             keptn/distributor:0.6.2                 run=distributor
```

```console
kubectl -n keptn-datastore get deployments -owide
```

```console
NAME                            READY   UP-TO-DATE   AVAILABLE   AGE   CONTAINERS          IMAGES                          SELECTOR
mongodb                         1/1     1            1           10m   mongodb             centos/mongodb-36-centos7:1     name=mongodb
mongodb-datastore               1/1     1            1           10m   mongodb-datastore   keptn/mongodb-datastore:0.6.1   run=mongodb-datastore
mongodb-datastore-distributor   1/1     1            1           10m   distributor         keptn/distributor:0.6.1         run=distributor
```

</details>

<details><summary>*Inspecting the upgrader logs*</summary>
To see the log of the upgrader, execute:

```
kubectl -n default logs job/upgrader
```

```
[keptn|DEBUG] [2020-04-29 11:40:40] Upgrading from Keptn 0.6.1 to 0.6.2
HTTP/1.1 200 OK
Cache-Control: max-age=300
Content-Security-Policy: default-src 'none'; style-src 'unsafe-inline'; sandbox
Content-Type: text/plain; charset=utf-8
Strict-Transport-Security: max-age=31536000
X-Content-Type-Options: nosniff
X-Frame-Options: deny
X-XSS-Protection: 1; mode=block
Via: 1.1 varnish (Varnish/6.0)
X-GitHub-Request-Id: 964C:369C:96CB0:C05FA:5EA967B8
Content-Length: 1008
Accept-Ranges: bytes
Date: Wed, 29 Apr 2020 11:40:40 GMT
Via: 1.1 varnish
Connection: keep-alive
X-Served-By: cache-mdw17337-MDW
X-Cache: MISS, MISS
X-Cache-Hits: 0, 0
X-Timer: S1588160441.776654,VS0,VE183
Vary: Authorization,Accept-Encoding
Access-Control-Allow-Origin: *
X-Fastly-Request-ID: e0c4cb1362edbbeb8bb7ffbd55e50418a01c6c28
Expires: Wed, 29 Apr 2020 11:45:40 GMT
Source-Age: 0

HTTP/1.1 200 OK
Cache-Control: max-age=300
Content-Security-Policy: default-src 'none'; style-src 'unsafe-inline'; sandbox
Content-Type: text/plain; charset=utf-8
Strict-Transport-Security: max-age=31536000
X-Content-Type-Options: nosniff
X-Frame-Options: deny
X-XSS-Protection: 1; mode=block
Via: 1.1 varnish (Varnish/6.0)
X-GitHub-Request-Id: 16C6:0D43:90CF5:B9F34:5EA967B5
Content-Length: 904
Accept-Ranges: bytes
Date: Wed, 29 Apr 2020 11:40:41 GMT
Via: 1.1 varnish
Connection: keep-alive
X-Served-By: cache-mdw17333-MDW
X-Cache: MISS, MISS
X-Cache-Hits: 0, 0
X-Timer: S1588160441.042223,VS0,VE95
Vary: Authorization,Accept-Encoding
Access-Control-Allow-Origin: *
X-Fastly-Request-ID: a42f1ed936f729fecfcebdfe1ab38a2df9de4663
Expires: Wed, 29 Apr 2020 11:45:41 GMT
Source-Age: 0

HTTP/1.1 200 OK
Cache-Control: max-age=300
Content-Security-Policy: default-src 'none'; style-src 'unsafe-inline'; sandbox
Content-Type: text/plain; charset=utf-8
Strict-Transport-Security: max-age=31536000
X-Content-Type-Options: nosniff
X-Frame-Options: deny
X-XSS-Protection: 1; mode=block
Via: 1.1 varnish (Varnish/6.0)
X-GitHub-Request-Id: D612:0D43:90CFB:B9F62:5EA967B9
Content-Length: 18013
Accept-Ranges: bytes
Date: Wed, 29 Apr 2020 11:40:41 GMT
Via: 1.1 varnish
Connection: keep-alive
X-Served-By: cache-pwk4977-PWK
X-Cache: MISS, MISS
X-Cache-Hits: 0, 0
X-Timer: S1588160441.236350,VS0,VE588
Vary: Authorization,Accept-Encoding
Access-Control-Allow-Origin: *
X-Fastly-Request-ID: a59e0d3b5833318503811f12cec31cf8b626b3a5
Expires: Wed, 29 Apr 2020 11:45:41 GMT
Source-Age: 0

HTTP/1.1 200 OK
Cache-Control: max-age=300
Content-Security-Policy: default-src 'none'; style-src 'unsafe-inline'; sandbox
Content-Type: text/plain; charset=utf-8
Strict-Transport-Security: max-age=31536000
X-Content-Type-Options: nosniff
X-Frame-Options: deny
X-XSS-Protection: 1; mode=block
Via: 1.1 varnish (Varnish/6.0)
X-GitHub-Request-Id: FF32:4894:9E22E:C999F:5EA967B9
Content-Length: 2060
Accept-Ranges: bytes
Date: Wed, 29 Apr 2020 11:40:42 GMT
Via: 1.1 varnish
Connection: keep-alive
X-Served-By: cache-mdw17382-MDW
X-Cache: MISS, MISS
X-Cache-Hits: 0, 0
X-Timer: S1588160442.899229,VS0,VE182
Vary: Authorization,Accept-Encoding
Access-Control-Allow-Origin: *
X-Fastly-Request-ID: d81c48694b33d5dec8183a734e7aaa05d454f1ca
Expires: Wed, 29 Apr 2020 11:45:42 GMT
Source-Age: 0

HTTP/1.1 200 OK
Cache-Control: max-age=300
Content-Security-Policy: default-src 'none'; style-src 'unsafe-inline'; sandbox
Content-Type: text/plain; charset=utf-8
Strict-Transport-Security: max-age=31536000
X-Content-Type-Options: nosniff
X-Frame-Options: deny
X-XSS-Protection: 1; mode=block
Via: 1.1 varnish (Varnish/6.0)
X-GitHub-Request-Id: 8F82:1DD2:98733:C3358:5EA967BA
Content-Length: 4381
Accept-Ranges: bytes
Date: Wed, 29 Apr 2020 11:40:42 GMT
Via: 1.1 varnish
Connection: keep-alive
X-Served-By: cache-pwk4947-PWK
X-Cache: MISS, MISS
X-Cache-Hits: 0, 0
X-Timer: S1588160442.177454,VS0,VE482
Vary: Authorization,Accept-Encoding
Access-Control-Allow-Origin: *
X-Fastly-Request-ID: f11ddeca5f000dd7b5d228edd95b6ce1eb378acc
Expires: Wed, 29 Apr 2020 11:45:42 GMT
Source-Age: 0

HTTP/1.1 200 OK
Cache-Control: max-age=300
Content-Security-Policy: default-src 'none'; style-src 'unsafe-inline'; sandbox
Content-Type: text/plain; charset=utf-8
Strict-Transport-Security: max-age=31536000
X-Content-Type-Options: nosniff
X-Frame-Options: deny
X-XSS-Protection: 1; mode=block
Via: 1.1 varnish (Varnish/6.0)
X-GitHub-Request-Id: AD94:4EC0:1DB4F:2529B:5EA967BA
Content-Length: 3876
Accept-Ranges: bytes
Date: Wed, 29 Apr 2020 11:40:42 GMT
Via: 1.1 varnish
Connection: keep-alive
X-Served-By: cache-mdw17375-MDW
X-Cache: MISS, MISS
X-Cache-Hits: 0, 0
X-Timer: S1588160443.732970,VS0,VE101
Vary: Authorization,Accept-Encoding
Access-Control-Allow-Origin: *
X-Fastly-Request-ID: abfca144d95a308587148d009e3c466a42806f49
Expires: Wed, 29 Apr 2020 11:45:42 GMT
Source-Age: 0

HTTP/1.1 200 OK
Cache-Control: max-age=300
Content-Security-Policy: default-src 'none'; style-src 'unsafe-inline'; sandbox
Content-Type: text/plain; charset=utf-8
Strict-Transport-Security: max-age=31536000
X-Content-Type-Options: nosniff
X-Frame-Options: deny
X-XSS-Protection: 1; mode=block
Via: 1.1 varnish (Varnish/6.0)
X-GitHub-Request-Id: 229E:5B8B:933BA:BC864:5EA967B9
Content-Length: 533
Accept-Ranges: bytes
Date: Wed, 29 Apr 2020 11:40:43 GMT
Via: 1.1 varnish
Connection: keep-alive
X-Served-By: cache-mdw17379-MDW
X-Cache: MISS, MISS
X-Cache-Hits: 0, 0
X-Timer: S1588160443.908553,VS0,VE172
Vary: Authorization,Accept-Encoding
Access-Control-Allow-Origin: *
X-Fastly-Request-ID: 16a56fd2e3c230450502aaf18f8c0c76a0831dca
Expires: Wed, 29 Apr 2020 11:45:43 GMT
Source-Age: 0

HTTP/1.1 200 OK
Cache-Control: max-age=300
Content-Security-Policy: default-src 'none'; style-src 'unsafe-inline'; sandbox
Content-Type: text/plain; charset=utf-8
Strict-Transport-Security: max-age=31536000
X-Content-Type-Options: nosniff
X-Frame-Options: deny
X-XSS-Protection: 1; mode=block
Via: 1.1 varnish (Varnish/6.0)
X-GitHub-Request-Id: A3EE:1DD1:49C1A:60233:5EA967B9
Content-Length: 579
Accept-Ranges: bytes
Date: Wed, 29 Apr 2020 11:40:43 GMT
Via: 1.1 varnish
Connection: keep-alive
X-Served-By: cache-mdw17376-MDW
X-Cache: MISS, MISS
X-Cache-Hits: 0, 0
X-Timer: S1588160443.155960,VS0,VE87
Vary: Authorization,Accept-Encoding
Access-Control-Allow-Origin: *
X-Fastly-Request-ID: f4f04812d631d76bbfd21b018709e72ad2964501
Expires: Wed, 29 Apr 2020 11:45:43 GMT
Source-Age: 0

HTTP/1.1 200 OK
Cache-Control: max-age=300
Content-Security-Policy: default-src 'none'; style-src 'unsafe-inline'; sandbox
Content-Type: text/plain; charset=utf-8
Strict-Transport-Security: max-age=31536000
X-Content-Type-Options: nosniff
X-Frame-Options: deny
X-XSS-Protection: 1; mode=block
Via: 1.1 varnish (Varnish/6.0)
X-GitHub-Request-Id: 8A54:416B:4D9C4:65343:5EA967B8
Content-Length: 967
Accept-Ranges: bytes
Date: Wed, 29 Apr 2020 11:40:43 GMT
Via: 1.1 varnish
Connection: keep-alive
X-Served-By: cache-mdw17382-MDW
X-Cache: MISS, MISS
X-Cache-Hits: 0, 0
X-Timer: S1588160443.321985,VS0,VE107
Vary: Authorization,Accept-Encoding
Access-Control-Allow-Origin: *
X-Fastly-Request-ID: b6efbe76c22b376e59d09606da50df5836629b4c
Expires: Wed, 29 Apr 2020 11:45:43 GMT
Source-Age: 0

HTTP/1.1 200 OK
Cache-Control: max-age=300
Content-Security-Policy: default-src 'none'; style-src 'unsafe-inline'; sandbox
Content-Type: text/plain; charset=utf-8
Strict-Transport-Security: max-age=31536000
X-Content-Type-Options: nosniff
X-Frame-Options: deny
X-XSS-Protection: 1; mode=block
Via: 1.1 varnish (Varnish/6.0)
X-GitHub-Request-Id: 1696:147C:1DBAE:24E56:5EA967BA
Content-Length: 854
Accept-Ranges: bytes
Date: Wed, 29 Apr 2020 11:40:43 GMT
Via: 1.1 varnish
Connection: keep-alive
X-Served-By: cache-pwk4959-PWK
X-Cache: MISS, MISS
X-Cache-Hits: 0, 0
X-Timer: S1588160444.506694,VS0,VE87
Vary: Authorization,Accept-Encoding
Access-Control-Allow-Origin: *
X-Fastly-Request-ID: 1da9f13b299021d793898c561f6ae46a112d2c6a
Expires: Wed, 29 Apr 2020 11:45:43 GMT
Source-Age: 0

[keptn|DEBUG] [2020-04-29 11:40:43] Check if Keptn 0.6.1 is currently installed
[keptn|DEBUG] [2020-04-29 11:40:43] Updating Keptn core.
configmap/api-nginx-config created
deployment.apps/api-gateway-nginx created
service/api-gateway-nginx created
deployment.apps/api-service created
service/api-service created
deployment.apps/bridge configured
service/bridge unchanged
deployment.apps/eventbroker-go configured
service/event-broker unchanged
deployment.apps/helm-service configured
service/helm-service unchanged
deployment.apps/helm-service-service-create-distributor configured
deployment.apps/shipyard-service configured
service/shipyard-service unchanged
deployment.apps/shipyard-service-create-project-distributor configured
deployment.apps/shipyard-service-delete-project-distributor configured
persistentvolumeclaim/configuration-volume configured
deployment.apps/configuration-service configured
service/configuration-service unchanged
deployment.apps/lighthouse-service configured
service/lighthouse-service unchanged
deployment.apps/lighthouse-service-distributor configured
deployment.extensions "api" deleted
service "api" deleted
Error from server (NotFound): namespaces "openshift" not found
NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)    AGE
gatekeeper-service   ClusterIP   10.72.4.71   <none>        8080/TCP   6m9s
[keptn|DEBUG] [2020-04-29 11:40:47] Full installation detected. Upgrading CD and CO services
deployment.apps/gatekeeper-service configured
service/gatekeeper-service unchanged
deployment.apps/gatekeeper-service-evaluation-done-distributor configured
deployment.apps/helm-service-configuration-change-distributor configured
deployment.apps/jmeter-service configured
service/jmeter-service unchanged
deployment.apps/jmeter-service-deployment-distributor configured
deployment.apps/wait-service configured
service/wait-service unchanged
deployment.apps/wait-service-deployment-distributor configured
deployment.apps/remediation-service configured
service/remediation-service unchanged
deployment.apps/remediation-service-problem-distributor configured
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   533  100   533    0     0   6126      0 --:--:-- --:--:-- --:--:--  6126
virtualservice.networking.istio.io/api configured
destinationrule.networking.istio.io/api-gateway-nginx created
Error from server (NotFound): services "dynatrace-service" not found
Error from server (NotFound): services "dynatrace-sli-service" not found
Error from server (NotFound): services "prometheus-service" not found
Error from server (NotFound): services "prometheus-sli-service" not found
Error from server (NotFound): services "servicenow-service" not found
```

**Note:** The messages at the end of the log output, such as `Error from server (NotFound): services "dynatrace-service" not found` does not mean that the upgrade has not been successful.
This message simply means that the respective service, e.g. the dynatrace-service has not been installed in your cluster in the previous Keptn version. 
If the service has indeed been deployed previously, it will be updated to the latest compatible version.
</details>

<details><summary>Upgrade didn't work, what to do next?</summary>

Please create a [new bug report](https://github.com/keptn/keptn/issues/new?assignees=&labels=bug&template=bug_report.md&title=) 
and provide us more information (log output, etc...), e.g.:

* `kubectl -n default logs job/upgrader`
* `kubectl get pods -n keptn`
* `kubectl -n keptn get deployments -owide`
* `kubectl get pods -n keptn-datastore`
* `kubectl -n keptn-datastore get deployments -owide`

</details>


## Upgrade from 0.6.0 to 0.6.1

* To download and install the Keptn CLI for version 0.6.1, please refer to the [Install Keptn CLI section](../setup-keptn/#install-keptn-cli).

* To upgrade your Keptn installation from 0.6.0 to 0.6.1, you can deploy a *Kubernetes Job* that will take care of updating all components to the 0.6.1 release. Please [verify that you are connected to the correct Kubernetes cluster](../../reference/troubleshooting/#verify-kubernetes-context-with-keptn-installation)
before deploying the upgrading job with the next command:

```console
kubectl -n default delete job upgrader
kubectl apply -f https://raw.githubusercontent.com/keptn/keptn/0.6.1/upgrade-060-061/upgrade-job.yaml
```

* To check the status of the update job, please execute:

```console
kubectl -n default get job
```
```
NAME                COMPLETIONS   DURATION   AGE
upgrader            1/1           17s        20h
```

When the job is completed, your Keptn version has been updated to 0.6.1.

<details><summary>*Verifying that the upgrade worked*</summary>

To verify that the upgrade process worked, please check the images and their tags using `kubectl` as described below. 

**Before the upgrade**:

```console
kubectl -n keptn get deployments -owide
```

```
NAME                                                      READY   UP-TO-DATE   AVAILABLE   AGE     CONTAINERS               IMAGES                                      SELECTOR
api                                                       1/1     1            1           4h25m   api                      keptn/api:0.6.0                             run=api
bridge                                                    1/1     1            1           4h25m   bridge                   keptn/bridge2:20200308.0859                 run=bridge
configuration-service                                     1/1     1            1           4h25m   configuration-service    keptn/configuration-service:20200308.0859   run=configuration-service
eventbroker-go                                            1/1     1            1           4h25m   eventbroker-go           keptn/eventbroker-go:0.6.0                  run=eventbroker-go
gatekeeper-service                                        1/1     1            1           4h24m   gatekeeper-service       keptn/gatekeeper-service:0.6.0              run=gatekeeper-service
gatekeeper-service-evaluation-done-distributor            1/1     1            1           4h24m   distributor              keptn/distributor:0.6.0                     run=distributor
helm-service                                              1/1     1            1           4h25m   helm-service             keptn/helm-service:0.6.0                    run=helm-service
helm-service-configuration-change-distributor             1/1     1            1           4h24m   distributor              keptn/distributor:0.6.0                     run=distributor
helm-service-service-create-distributor                   1/1     1            1           4h25m   distributor              keptn/distributor:0.6.0                     run=distributor
jmeter-service                                            1/1     1            1           4h24m   jmeter-service           keptn/jmeter-service:0.6.0                  run=jmeter-service
jmeter-service-deployment-distributor                     1/1     1            1           4h24m   distributor              keptn/distributor:0.6.0                     run=distributor
lighthouse-service                                        1/1     1            1           4h24m   lighthouse-service       keptn/lighthouse-service:0.6.0              run=lighthouse-service
lighthouse-service-get-sli-done-distributor               1/1     1            1           4h24m   distributor              keptn/distributor:0.6.0                     run=distributor
lighthouse-service-start-evaluation-distributor           1/1     1            1           4h24m   distributor              keptn/distributor:0.6.0                     run=distributor
lighthouse-service-tests-finished-distributor             1/1     1            1           4h24m   distributor              keptn/distributor:0.6.0                     run=distributor
nats-operator                                             1/1     1            1           4h25m   nats-operator            connecteverything/nats-operator:0.6.0       name=nats-operator
prometheus-service                                        1/1     1            1           27m     prometheus-service       keptn/prometheus-service:0.3.1              run=prometheus-service
prometheus-service-monitoring-configure-distributor       1/1     1            1           27m     distributor              keptn/distributor:0.5.0                     run=distributor
prometheus-sli-service                                    1/1     1            1           24m     prometheus-sli-service   keptn/prometheus-sli-service:0.2.0          run=prometheus-sli-service
prometheus-sli-service-monitoring-configure-distributor   1/1     1            1           24m     distributor              keptn/distributor:0.5.0                     run=distributor
remediation-service                                       1/1     1            1           4h24m   remediation-service      keptn/remediation-service:0.6.0             run=remediation-service
remediation-service-problem-distributor                   1/1     1            1           4h24m   distributor              keptn/distributor:0.6.0                     run=distributor
shipyard-service                                          1/1     1            1           4h25m   shipyard-service         keptn/shipyard-service:0.6.0                run=shipyard-service
shipyard-service-create-project-distributor               1/1     1            1           4h25m   distributor              keptn/distributor:0.6.0                     run=distributor
shipyard-service-delete-project-distributor               1/1     1            1           4h25m   distributor              keptn/distributor:0.6.0                     run=distributor
wait-service                                              1/1     1            1           4h24m   wait-service             keptn/wait-service:0.6.0                    run=wait-service
wait-service-deployment-distributor                       1/1     1            1           4h24m   distributor              keptn/distributor:0.6.0                     run=distributor
```

```console
kubectl -n keptn-datastore get deployments -owide
```

```console
NAME                            READY   UP-TO-DATE   AVAILABLE   AGE     CONTAINERS          IMAGES                                  SELECTOR
mongodb                         1/1     1            1           4h25m   mongodb             centos/mongodb-36-centos7:1             name=mongodb
mongodb-datastore               1/1     1            1           4h25m   mongodb-datastore   keptn/mongodb-datastore:20200308.0859   run=mongodb-datastore
mongodb-datastore-distributor   1/1     1            1           4h25m   distributor         keptn/distributor:0.6.0                 run=distributor
```

**After the upgrade**

```console
kubectl -n keptn get deployments -owide
```

```console
NAME                                                      READY   UP-TO-DATE   AVAILABLE   AGE     CONTAINERS               IMAGES                                  SELECTOR
api                                                       1/1     1            1           4h39m   api                      keptn/api:0.6.1                         run=api
bridge                                                    1/1     1            1           4h39m   bridge                   keptn/bridge2:0.6.1                     run=bridge
configuration-service                                     1/1     1            1           4h39m   configuration-service    keptn/configuration-service:0.6.1       run=configuration-service
eventbroker-go                                            1/1     1            1           4h39m   eventbroker-go           keptn/eventbroker-go:0.6.1              run=eventbroker-go
gatekeeper-service                                        1/1     1            1           4h39m   gatekeeper-service       keptn/gatekeeper-service:0.6.1          run=gatekeeper-service
gatekeeper-service-evaluation-done-distributor            1/1     1            1           4h39m   distributor              keptn/distributor:0.6.1                 run=distributor
helm-service                                              1/1     1            1           4h39m   helm-service             keptn/helm-service:0.6.1                run=helm-service
helm-service-configuration-change-distributor             1/1     1            1           4h39m   distributor              keptn/distributor:0.6.1                 run=distributor
helm-service-service-create-distributor                   1/1     1            1           4h39m   distributor              keptn/distributor:0.6.1                 run=distributor
jmeter-service                                            1/1     1            1           4h39m   jmeter-service           keptn/jmeter-service:0.6.1              run=jmeter-service
jmeter-service-deployment-distributor                     1/1     1            1           4h39m   distributor              keptn/distributor:0.6.1                 run=distributor
lighthouse-service                                        1/1     1            1           4h39m   lighthouse-service       keptn/lighthouse-service:0.6.1          run=lighthouse-service
lighthouse-service-distributor                            1/1     1            1           72s     distributor              keptn/distributor:0.6.1                 run=distributor
nats-operator                                             1/1     1            1           4h40m   nats-operator            connecteverything/nats-operator:0.6.0   name=nats-operator
prometheus-service                                        1/1     1            1           41m     prometheus-service       keptn/prometheus-service:0.3.1          run=prometheus-service
prometheus-service-monitoring-configure-distributor       1/1     1            1           41m     distributor              keptn/distributor:0.5.0                 run=distributor
prometheus-sli-service                                    1/1     1            1           38m     prometheus-sli-service   keptn/prometheus-sli-service:0.2.1      run=prometheus-sli-service
prometheus-sli-service-monitoring-configure-distributor   1/1     1            1           38m     distributor              keptn/distributor:latest                run=distributor
remediation-service                                       1/1     1            1           4h39m   remediation-service      keptn/remediation-service:0.6.1         run=remediation-service
remediation-service-problem-distributor                   1/1     1            1           4h39m   distributor              keptn/distributor:0.6.1                 run=distributor
shipyard-service                                          1/1     1            1           4h39m   shipyard-service         keptn/shipyard-service:0.6.1            run=shipyard-service
shipyard-service-create-project-distributor               1/1     1            1           4h39m   distributor              keptn/distributor:0.6.1                 run=distributor
shipyard-service-delete-project-distributor               1/1     1            1           4h39m   distributor              keptn/distributor:0.6.1                 run=distributor
wait-service                                              1/1     1            1           4h39m   wait-service             keptn/wait-service:0.6.1                run=wait-service
wait-service-deployment-distributor                       1/1     1            1           4h39m   distributor              keptn/distributor:0.6.1                 run=distributor

```

```console
kubectl -n keptn-datastore get deployments -owide
```

```console
NAME                            READY   UP-TO-DATE   AVAILABLE   AGE     CONTAINERS          IMAGES                          SELECTOR
mongodb                         1/1     1            1           2m41s   mongodb             centos/mongodb-36-centos7:1     name=mongodb
mongodb-datastore               1/1     1            1           4h40m   mongodb-datastore   keptn/mongodb-datastore:0.6.1   run=mongodb-datastore
mongodb-datastore-distributor   1/1     1            1           4h40m   distributor         keptn/distributor:0.6.1         run=distributor
```

</details>

<details><summary>*Inspecting the upgrader logs*</summary>
To see the log of the upgrader, execute:

```
kubectl -n default logs job/upgrader
```

The expected log output should look as follows:

```
X-Content-Type-Options: nosniff
X-Frame-Options: deny
X-XSS-Protection: 1; mode=block
Cache-Control: max-age=300
X-Geo-Block-List:
Via: 1.1 varnish (Varnish/6.0)
X-GitHub-Request-Id: EA38:03B6:2FB4D:40878:5E68D9A4
Content-Length: 185
Accept-Ranges: bytes
Date: Wed, 11 Mar 2020 12:29:27 GMT
Via: 1.1 varnish
Connection: keep-alive
X-Served-By: cache-mdw17332-MDW
X-Cache: MISS, MISS
X-Cache-Hits: 0, 0
X-Timer: S1583929768.602904,VS0,VE141
Vary: Authorization,Accept-Encoding
Access-Control-Allow-Origin: *
X-Fastly-Request-ID: 9dd59ca82cfb8b58daeccf1c941cda68f0c41559
Expires: Wed, 11 Mar 2020 12:34:27 GMT
Source-Age: 0

HTTP/1.1 200 OK
Content-Type: text/plain; charset=utf-8
Content-Security-Policy: default-src 'none'; style-src 'unsafe-inline'; sandbox
Strict-Transport-Security: max-age=31536000
X-Content-Type-Options: nosniff
X-Frame-Options: deny
X-XSS-Protection: 1; mode=block
Cache-Control: max-age=300
X-Geo-Block-List:
Via: 1.1 varnish (Varnish/6.0)
X-GitHub-Request-Id: 14EA:2261:5CD15:7C5E6:5E68D9A7
Content-Length: 931
Accept-Ranges: bytes
Date: Wed, 11 Mar 2020 12:29:27 GMT
Via: 1.1 varnish
Connection: keep-alive
X-Served-By: cache-mdw17354-MDW
X-Cache: MISS, MISS
X-Cache-Hits: 0, 0
X-Timer: S1583929768.815580,VS0,VE119
Vary: Authorization,Accept-Encoding
Access-Control-Allow-Origin: *
X-Fastly-Request-ID: 5a6a439ec8e8dd3baa8eb976e3ec4c7311afb3a6
Expires: Wed, 11 Mar 2020 12:34:27 GMT
Source-Age: 0

HTTP/1.1 200 OK
Content-Type: text/plain; charset=utf-8
Content-Security-Policy: default-src 'none'; style-src 'unsafe-inline'; sandbox
Strict-Transport-Security: max-age=31536000
X-Content-Type-Options: nosniff
X-Frame-Options: deny
X-XSS-Protection: 1; mode=block
Cache-Control: max-age=300
X-Geo-Block-List:
Via: 1.1 varnish (Varnish/6.0)
X-GitHub-Request-Id: BAA4:61F0:329AB:43B6A:5E68D9A6
Content-Length: 185
Accept-Ranges: bytes
Date: Wed, 11 Mar 2020 12:29:28 GMT
Via: 1.1 varnish
Connection: keep-alive
X-Served-By: cache-mdw17347-MDW
X-Cache: MISS, MISS
X-Cache-Hits: 0, 0
X-Timer: S1583929768.007367,VS0,VE122
Vary: Authorization,Accept-Encoding
Access-Control-Allow-Origin: *
X-Fastly-Request-ID: db1cbe1861e8c02f6915c6cf08276cf3583b3543
Expires: Wed, 11 Mar 2020 12:34:28 GMT
Source-Age: 0

HTTP/1.1 200 OK
Content-Type: text/plain; charset=utf-8
Content-Security-Policy: default-src 'none'; style-src 'unsafe-inline'; sandbox
Strict-Transport-Security: max-age=31536000
X-Content-Type-Options: nosniff
X-Frame-Options: deny
X-XSS-Protection: 1; mode=block
Cache-Control: max-age=300
X-Geo-Block-List:
Via: 1.1 varnish (Varnish/6.0)
X-GitHub-Request-Id: 7F68:7400:66E52:87C3C:5E68D9A8
Content-Length: 9180
Accept-Ranges: bytes
Date: Wed, 11 Mar 2020 12:29:28 GMT
Via: 1.1 varnish
Connection: keep-alive
X-Served-By: cache-mdw17346-MDW
X-Cache: MISS, MISS
X-Cache-Hits: 0, 0
X-Timer: S1583929768.229165,VS0,VE109
Vary: Authorization,Accept-Encoding
Access-Control-Allow-Origin: *
X-Fastly-Request-ID: 4dbedcfa191cbe06b8db7314ef1f6cac911dcabc
Expires: Wed, 11 Mar 2020 12:34:28 GMT
Source-Age: 0

HTTP/1.1 200 OK
Content-Type: text/plain; charset=utf-8
Content-Security-Policy: default-src 'none'; style-src 'unsafe-inline'; sandbox
Strict-Transport-Security: max-age=31536000
X-Content-Type-Options: nosniff
X-Frame-Options: deny
X-XSS-Protection: 1; mode=block
Cache-Control: max-age=300
X-Geo-Block-List:
Via: 1.1 varnish (Varnish/6.0)
X-GitHub-Request-Id: E6C6:26D5:A1F2:EBC2:5E68D9A7
Content-Length: 2060
Accept-Ranges: bytes
Date: Wed, 11 Mar 2020 12:29:28 GMT
Via: 1.1 varnish
Connection: keep-alive
X-Served-By: cache-mdw17338-MDW
X-Cache: MISS, MISS
X-Cache-Hits: 0, 0
X-Timer: S1583929768.410886,VS0,VE150
Vary: Authorization,Accept-Encoding
Access-Control-Allow-Origin: *
X-Fastly-Request-ID: c40bed9f09e89a884ccfb50b7a06e01992fdfe29
Expires: Wed, 11 Mar 2020 12:34:28 GMT
Source-Age: 0

HTTP/1.1 200 OK
Content-Type: text/plain; charset=utf-8
Content-Security-Policy: default-src 'none'; style-src 'unsafe-inline'; sandbox
Strict-Transport-Security: max-age=31536000
X-Content-Type-Options: nosniff
X-Frame-Options: deny
X-XSS-Protection: 1; mode=block
Cache-Control: max-age=300
X-Geo-Block-List:
Via: 1.1 varnish (Varnish/6.0)
X-GitHub-Request-Id: 4CF2:1FEB:5D0AD:7C5E8:5E68D9A7
Content-Length: 4381
Accept-Ranges: bytes
Date: Wed, 11 Mar 2020 12:29:28 GMT
Via: 1.1 varnish
Connection: keep-alive
X-Served-By: cache-mdw17345-MDW
X-Cache: MISS, MISS
X-Cache-Hits: 0, 0
X-Timer: S1583929769.632244,VS0,VE100
Vary: Authorization,Accept-Encoding
Access-Control-Allow-Origin: *
X-Fastly-Request-ID: 592cdff071a491a9b6dc3f432e711a19273d45ea
Expires: Wed, 11 Mar 2020 12:34:28 GMT
Source-Age: 0

HTTP/1.1 200 OK
Content-Type: text/plain; charset=utf-8
Content-Security-Policy: default-src 'none'; style-src 'unsafe-inline'; sandbox
Strict-Transport-Security: max-age=31536000
X-Content-Type-Options: nosniff
X-Frame-Options: deny
X-XSS-Protection: 1; mode=block
Cache-Control: max-age=300
X-Geo-Block-List:
Via: 1.1 varnish (Varnish/6.0)
X-GitHub-Request-Id: C12E:6C2D:66F73:88323:5E68D9A7
Content-Length: 3876
Accept-Ranges: bytes
Date: Wed, 11 Mar 2020 12:29:28 GMT
Via: 1.1 varnish
Connection: keep-alive
X-Served-By: cache-mdw17343-MDW
X-Cache: MISS, MISS
X-Cache-Hits: 0, 0
X-Timer: S1583929769.802585,VS0,VE84
Vary: Authorization,Accept-Encoding
Access-Control-Allow-Origin: *
X-Fastly-Request-ID: ffb1f45f5f9b495b53c9737294bdcceaab6b18bc
Expires: Wed, 11 Mar 2020 12:34:28 GMT
Source-Age: 0

[keptn|DEBUG] [2020-03-11 12:29:28] Check if Keptn 0.6.0 is currently installed
[keptn|DEBUG] [2020-03-11 12:29:29] Exporting events from previous Keptn installation.
2020-03-11T12:29:29.345+0000    connected to: localhost
2020-03-11T12:29:29.369+0000    exported 208 records
[keptn|DEBUG] [2020-03-11 12:29:29] Updating MongoDB.
deployment.extensions "mongodb" deleted
persistentvolumeclaim/mongodata configured
deployment.apps/mongodb created
service/mongodb configured
Waiting for deployment "mongodb" rollout to finish: 0 of 1 updated replicas are available...
deployment "mongodb" successfully rolled out
[keptn|DEBUG] [2020-03-11 12:29:34] Deployment mongodb in keptn-datastore namespace available.
deployment "mongodb" successfully rolled out
[keptn|DEBUG] [2020-03-11 12:29:34] Deployment mongodb-datastore in keptn-datastore namespace available.
deployment "mongodb" successfully rolled out
[keptn|DEBUG] [2020-03-11 12:29:34] Deployment mongodb-datastore-distributor in keptn-datastore namespace available.
[keptn|DEBUG] [2020-03-11 12:29:34] Importing events from previous installation to updated MongoDB.
2020-03-11T12:29:37.691+0000    [........................] keptn.events 0B/110KB (0.0%)
2020-03-11T12:29:37.742+0000    connected to: localhost
2020-03-11T12:29:37.768+0000    [########################] keptn.events 110KB/110KB (100.0%)
2020-03-11T12:29:37.768+0000    imported 208 documents
[keptn|DEBUG] [2020-03-11 12:29:37] Updating mongodb-datastore.
deployment.extensions/mongodb-datastore image updated
deployment.extensions/mongodb-datastore-distributor image updated
[keptn|DEBUG] [2020-03-11 12:29:37] Updating Keptn core.
deployment.apps/api configured
service/api unchanged
deployment.apps/bridge configured
service/bridge unchanged
deployment.apps/eventbroker-go configured
service/event-broker unchanged
deployment.apps/helm-service configured
service/helm-service unchanged
deployment.apps/helm-service-service-create-distributor configured
deployment.apps/shipyard-service configured
service/shipyard-service unchanged
deployment.apps/shipyard-service-create-project-distributor configured
deployment.apps/shipyard-service-delete-project-distributor configured
persistentvolumeclaim/configuration-volume configured
deployment.apps/configuration-service configured
service/configuration-service unchanged
deployment.apps/lighthouse-service configured
service/lighthouse-service unchanged
deployment.apps/lighthouse-service-distributor created
NAME                 TYPE        CLUSTER-IP    EXTERNAL-IP   PORT(S)    AGE
gatekeeper-service   ClusterIP   10.48.2.161   <none>        8080/TCP   7d20h
[keptn|DEBUG] [2020-03-11 12:29:40] Full installation detected. Upgrading CD and CO services
deployment.apps/gatekeeper-service configured
service/gatekeeper-service unchanged
deployment.apps/gatekeeper-service-evaluation-done-distributor configured
deployment.apps/helm-service-configuration-change-distributor configured
deployment.apps/jmeter-service configured
service/jmeter-service unchanged
deployment.apps/jmeter-service-deployment-distributor configured
deployment.apps/wait-service configured
service/wait-service unchanged
deployment.apps/wait-service-deployment-distributor configured
deployment.apps/remediation-service configured
service/remediation-service unchanged
deployment.apps/remediation-service-problem-distributor configured
Error from server (NotFound): services "dynatrace-service" not found
Error from server (NotFound): services "dynatrace-sli-service" not found
Error from server (NotFound): services "prometheus-service" not found
Error from server (NotFound): services "prometheus-sli-service" not found
Error from server (NotFound): services "servicenow-service" not found
```

**Note:** The messages at the end of the log output, such as `Error from server (NotFound): services "dynatrace-service" not found` does not mean that the upgrade has not been successful.
This message simply means that the respective service, e.g. the dynatrace-service has not been installed in your cluster in the previous Keptn version. 
If the service has indeed been deployed previously, it will be updated to the latest compatible version.
</details>

<details><summary>Upgrade didn't work, what to do next?</summary>

Please create a [new bug report](https://github.com/keptn/keptn/issues/new?assignees=&labels=bug&template=bug_report.md&title=) 
and provide us more information (log output, etc...), e.g.:

* `kubectl -n default logs job/upgrader`
* `kubectl get pods -n keptn`
* `kubectl -n keptn get deployments -owide`
* `kubectl get pods -n keptn-datastore`
* `kubectl -n keptn-datastore get deployments -owide`

</details>

## Upgrade from 0.6.0beta(2) to 0.6.0

When we introduced the new lighthouse-service with custom SLIs in 0.6.0.beta we got a lot of feedback. We value this feedback, and we wanted to thank all our beta testers for their extensive testing and feedback provided by providing an upgrade guide from 0.6.0.beta(2) to 0.6.0.

### Custom SLIs in Git repo

For Keptn 0.6.0.beta(2), custom SLIs were configured by creating a Kubernetes ConfigMap for Prometheus that looked like this:

```yaml
apiVersion: v1
data:
  custom-queries: |
    cpu_usage: avg(rate(container_cpu_usage_seconds_total{namespace="$PROJECT-$STAGE",pod_name=~"$SERVICE-primary-.*"}[5m]))
    response_time_p95: histogram_quantile(0.95, sum by(le) (rate(http_response_time_milliseconds_bucket{handler="ItemsController.addToCart",job="$SERVICE-$PROJECT-$STAGE"}[$DURATION_SECONDS])))
kind: ConfigMap
metadata:
  name: prometheus-sli-config-sockshop
  namespace: keptn
```

With Keptn 0.6.0, custom SLIs need to be added for the project/service/stage by using [keptn add-resource](../../reference/cli/commands/keptn_add-resource). With this change in mind, we also had to slightly adapt the format of the file. Above file would now look as follows:

```yaml
---
spec_version: '1.0'
indicators:
  cpu_usage: avg(rate(container_cpu_usage_seconds_total{namespace="$PROJECT-$STAGE",pod_name=~"$SERVICE-primary-.*"}[5m]))
  response_time_p95: histogram_quantile(0.95, sum by(le) (rate(http_response_time_milliseconds_bucket{handler="ItemsController.addToCart",job="$SERVICE-$PROJECT-$STAGE"}[$DURATION_SECONDS])))
```

To migrate from the old format to the new format, you can:

1. Fetch the ConfigMap using ` kubectl get configmap -n keptn prometheus-sli-config-sockshop -oyaml`
1. Copy the content from within the `custom-queries: |` section (without `custom-queries: |`)
1. Create a new file called `sli.yaml` with the following content:

    ```yaml
    ---
    spec_version: '1.0'
    indicators:
      # paste-content-here
    ```

The newly created file needs to be added to as follows:

* Prometheus

```console
keptn add-resource --project=sockshop --stage=staging --service=carts --resource=sli.yaml --resourceUri=prometheus/sli.yaml
```

* Dynatrace

```console
keptn add-resource --project=sockshop --stage=staging --service=carts --resource=sli.yaml --resourceUri=dynatrace/sli.yaml
```

### Ingress Gateway

If you want to stay compatible, you need to perform the following steps:

1. Delete the existing gateways that are relevant for Keptn namespace using:
```console
kubectl delete gateway keptn-gateway -n keptn
```

1. Apply the new public-gateway in namespace istio-system using:
```console
kubectl apply -f https://raw.githubusercontent.com/keptn/keptn/release-0.6.0/installer/manifests/istio/public-gateway.yaml
```

1. Edit the VirtualService for the Keptn api service such that it uses `public-gateway.istio-system` instead of `keptn-gateway`: 
```console
kubectl get vs/api -n keptn -o yaml | sed 's/keptn-gateway/public-gateway.istio-system/g' | kubectl replace -f -
```

1. Verify that you can still access the API via a browser.

1. Adapt all VirtualServices of onboarded services to use the `public-gateway.istio-system` (e.g., by sending a `new-artifact` event for all those services which will be handled by the updated helm-service, or by manually editing the virtual services)

1. (Optional) Delete all generated gateways (in all namespaces of the project-stages) using: `kubectl delete gateways -n $project-$stage` for every $project and $stage)

### Upgrade services

Please [verify that you are connected to the correct Kubernetes cluster](../../reference/troubleshooting/#verify-kubernetes-context-with-keptn-installation)
before performing this operation.

**Update services in keptn-datastore namespace**

```console
kubectl -n keptn-datastore set image deployment/mongodb-datastore mongodb-datastore=keptn/mongodb-datastore:0.6.0 --record
kubectl -n keptn-datastore set image deployment/mongodb-datastore-distributor distributor=keptn/distributor:0.6.0 --record
```

**Update services in keptn namespace**

```console
kubectl apply -f https://raw.githubusercontent.com/keptn/keptn/release-0.6.0/installer/manifests/keptn/core.yaml
kubectl apply -f https://raw.githubusercontent.com/keptn/keptn/release-0.6.0/installer/manifests/keptn/continuous-deployment.yaml
kubectl apply -f https://raw.githubusercontent.com/keptn/keptn/release-0.6.0/installer/manifests/keptn/quality-gates.yaml
kubectl apply -f https://raw.githubusercontent.com/keptn/keptn/release-0.6.0/installer/manifests/keptn/continuous-operations.yaml
```

**Update keptn-contrib services** 

Please [verify that you are connected to the correct Kubernetes cluster](../../reference/troubleshooting/#verify-kubernetes-context-with-keptn-installation)
before performing this operation.

Also, only update the services if you have them installed:

* *dynatrace-service*: `kubectl apply -f https://raw.githubusercontent.com/keptn-contrib/dynatrace-service/release-0.6.0/deploy/manifests/dynatrace-service/dynatrace-service.yaml`
* *dynatrace-sli-service*: `kubectl apply -f https://raw.githubusercontent.com/keptn-contrib/dynatrace-sli-service/release-0.3.0/deploy/service.yaml`
* *prometheus-service*: `kubectl apply -f https://raw.githubusercontent.com/keptn-contrib/prometheus-service/release-0.3.1/deploy/service.yaml`
* *prometheus-sli-service*: `kubectl apply -f https://raw.githubusercontent.com/keptn-contrib/prometheus-sli-service/release-0.2.0/deploy/service.yaml`
* *notification-service*: `kubectl -n keptn set image deployment/notification-service notification-service=keptncontrib/notification-service:0.3.0 --record`

## Upgrade from 0.5.x to 0.6.0

For full details on what has changed from Keptn 0.5.x to Keptn 0.6.0 please refer to the release notes within the [Keptn repository](https://github.com/keptn/keptn/releases/0.6.0). 

Unfortunately, there are multiple breaking changes from Keptn 0.5.x to Keptn 0.6.x that make it impossible to provide an upgrade script from Keptn 0.5.x to Keptn 0.6.x. These breaking changes include:

* Istio sidecar injection has been introduced for blue-green deployments
* Pitometer was removed, instead the lighthouse was installed
* Ingress gateway handling was changed

Instead of an upgrade script, we will highlight the most important changes that you need to do to get your services onboarded with a fresh Keptn 0.6.0 installation.

**Note:** Advise for migrating from [Keptn 0.6.0.beta(2) to 0.6.0](#upgrade-from-0-6-0beta-2-to-0-6-0) is listed above.

### Helm Charts

Several changes to Helm charts have been made. If you want to stay compatible, please adapt your Helm charts accordingly.

* Parameterize the `replicas` in the deployment manifest. Therefore, set `replicas: {{ .Values.replicaCount }}` instead of a fixed value, e.g.: `replicas: 1`:

  ```yaml
  replicas: {{ .Values.replicaCount }}
  ```

  See example: https://github.com/keptn/examples/blob/release-0.6.0/onboarding-carts/carts/templates/deployment.yaml#L7

* Then, set a new value in `values.yaml` for each service: `replicaCount`. 

  See example: https://github.com/keptn/examples/blob/release-0.6.0/onboarding-carts/carts/values.yaml

* Dynatrace integration: We have removed `DT_TAGS` and introduced `DT_CUSTOM_PROP`:

  ```yaml
  - name: DT_CUSTOM_PROP
    value: "keptn_project={{ .Values.keptn.project }} keptn_service={{ .Values.keptn.service }} keptn_stage={{ .Values.keptn.stage }} keptn_deployment={{ .Values.keptn.deployment }}"
  ```
  
  See example: https://github.com/keptn/examples/blob/release-0.6.0/onboarding-carts/carts/templates/deployment.yaml#L29-L30

### New Lighthouse / Pitometer was removed

Pitometer was removed including the support for PerfSpec files. Instead, a new service called *lighthouse* has been introduced. Please follow the [Deployment with Quality Gates](../../usecases/deployments-with-quality-gates/) tutorial to learn more about the new file formats used for quality gates.
