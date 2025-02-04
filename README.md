[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://github.com/chen-keinan/openshift-ordeal/blob/main/LICENSE)
<img src="./pkg/img/coverage_badge.png" alt="test coverage badge">
[![Gitter](https://badges.gitter.im/beacon-sec/openshift-ordeal.svg)](https://gitter.im/beacon-sec/openshift-ordeal?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)
<br><img src="./pkg/img/openshift-ordeal.png" width="300" alt="openshift-ordeal logo"><br>
# OpenShift-Ordeal

###  Scan your Openshift cluster !!
OpenShift-Ordeal is an open source audit scanner who perform audit check on OpenShift Cluster and output it security report.

The audit tests are the full implementation of [CIS openshift Benchmark specification](https://www.cisecurity.org/benchmark/openshift/) <br>

audit result now can be leveraged as webhook via user plugin(using go plugin)
#### Audit checks are performed on OpenShift cluster, and output audit report include :
 1.  root cause of the security issue.
 2. proposed remediation for security issue

#### Openshift cluster scan output:


--------------------------------------------------------------------------------------------------------

* [Installation](#installation)
* [Quick Start](#quick-start)
* [User Plugin Usage](#user-plugin-usage)
* [Supported Specs](#supported-specs)
* [Contribution](#Contribution)

## Installation

```
git clone https://github.com/chen-keinan/openshift-ordeal
cd openshift-ordeal
make build
./openshift-ordeal
```

Note : openshift-ordeal require privileged user to execute tests.

## Quick Start

```
Usage: openshift-ordeal [--version] [--help] <command> [<args>]

Available commands are:
  -r , --report :  run audit tests and generate failure and warn report
  -i , --include:  execute only specific audit test,   example -i=1.2.3,1.4.5
  -e , --exclude:  ignore specific audit tests,  example -e=1.2.3,1.4.5
  -c , --classic:  test report in classic view,  example -c

```
## User Plugin Usage
The openshift-ordeal expose hook for user plugins [Example](https://github.com/chen-keinan/openshift-ordeal/tree/master/examples/plugins) :
- **openshiftBenchAuditResultHook** - this hook accepts audit benchmark results as found by audit test

##### Compile user plugin
```
go build -buildmode=plugin -o=~/<plugin folder>/bench_plugin.so /<plugin folder>/bench_plugin.go
```
##### Copy plugin to folder (.openshift-ordeal folder is created on the 1st startup)
```
cp /<plugin folder>/bench_plugin.so ~/.openshift-ordeal/plugins/compile/bench_plugin.so
```
Note: Plugin and binary must compile with the same linux env
## Supported Specs
The openshift-ordeal support cis specs and can be easily extended:
- master config file change spec [CIS openshift Benchmark specification](https://www.cisecurity.org/benchmark/openshift/)
both specs can be easily extended by amended the spec files under ```~/.openshift-ordeal/benchmarks/openshift/v1.0.0``` folder

## Contribution
- code contribution is welcome !! , contribution with tests and passing linter is more than welcome :)
- /.dev folder include vagrantfile to be used for development : [Dev Instruction](https://github.com/chen-keinan/openshift-ordeal/tree/master/.dev)
