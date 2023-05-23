# Magento Test Environment Helm Chart

This Helm chart deploys a Magento test environment consisting of several services running on Kubernetes.

## Prerequisites

- Kubernetes cluster up and running
- Helm 3 or later installed
- Docker registry set up to push and pull container images (optional)

## Installation

1. Clone the repository:

```shell
git clone <repository-url>
```

2. Build the PHP Docker Image
```shell
cd magento-test-env/charts/php/templates
./build-php-image.sh
```

This step is optional if you already have a pre-built PHP image available in your registry.

3. Push the PHP Docker image to your Docker registry (optional):
docker push your-docker-repo/your-php-image:tag

Skip this step if you're using a pre-built PHP image or planning to build it directly within the cluster.

4. Install the Helm chart:

```shell
helm install magento-test-env ./magento-test-env
```
This will deploy the Magento test environment with default configurations. You can modify the values in values.yaml as needed.

### Configuration
The following table lists the configurable parameters of the Helm chart:

| Parameter                    | Description                               | Default                              |
|------------------------------|-------------------------------------------|--------------------------------------|
| `image.repository`           | PHP image repository                       | `your-docker-repo`                   |
| `image.tag`                  | PHP image tag                              | `tag`                                |
| `varnish.enabled`            | Enable Varnish deployment                  | `true`                               |
| `varnish.replicaCount`       | Number of Varnish replicas                 | `1`                                  |
| `varnish.image.repository`   | Varnish image repository                   | `your-varnish-repo`                  |
| `varnish.image.tag`          | Varnish image tag                          | `varnish-tag`                        |
| `mysql.enabled`              | Enable MySQL deployment                     | `true`                               |
| `mysql.replicaCount`         | Number of MySQL replicas                    | `1`                                  |
| `mysql.image.repository`     | MySQL image repository                     | `mysql`                              |
| `mysql.image.tag`            | MySQL image tag                            | `latest`                             |
| `mysql.rootPassword`         | Root password for MySQL                     | `password`                           |
| `elasticsearch.enabled`      | Enable Elasticsearch deployment            | `true`                               |
| `elasticsearch.replicaCount` | Number of Elasticsearch replicas           | `1`                                  |
| `elasticsearch.image.repository` | Elasticsearch image repository           | `elasticsearch`                      |
| `elasticsearch.image.tag`    | Elasticsearch image tag                    | `7.10.1`                             |
| `registry.enabled`           | Enable Docker Registry deployment          | `true`                               |
| `registry.replicaCount`      | Number of Docker Registry replicas         | `1`                                  |
| `registry.image.repository`  | Docker Registry image repository           | `registry`                           |
| `registry.image.tag`         | Docker Registry image tag                  | `2`                                  |
| ...                          | ...                                       | ...                                  |

You can modify these parameters in the values.yaml file or override them during the Helm installation.

### Cleanup
To remove the Magento test environment deployment, run the following command:

```shell
helm uninstall magento-test-env
```

### Customization
This Helm chart provides a starting point for deploying a Magento test environment. You can customize the chart according to your specific requirements by modifying the template files and values.

For more details on how to customize Helm charts, refer to the [Helm documentation](https://helm.sh/docs/).

### License
This Helm chart is released under the [MIT License](https://chat.openai.com/c/LICENSE).
