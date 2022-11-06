# MySQL Operator ARM64 Charts

This is mostly a convenience Helm repository for ARM64 builds. `mysql-operator` charts in this repo
defines GHCR as the image registry, `canozokur` as the image repository.

`mysql-innodb-cluster` chart adds the ability to override `router` podSpec with a custom one. Operator's own
CRDs allow this already but for some reason the original repo didn't include it in their Helm charts.

## Usage

[Helm](https://helm.sh) must be installed to use the charts.  Please refer to
Helm's [documentation](https://helm.sh/docs) to get started.

Once Helm has been set up correctly, add the repo as follows:

    helm repo add mysql-operator-arm64 https://canozokur.github.io/mysql-operator


If you had already added this repo earlier, run `helm repo update` to retrieve
the latest versions of the packages.  You can then run `helm search repo
mysql-operator-arm64` to see the charts.

To install the mysql-operator chart:

    helm install my-mysql-operator mysql-operator-arm64/mysql-operator

To uninstall the chart:

    helm delete my-mysql-operator
