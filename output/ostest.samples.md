# Manually Collected Output Samples

## Miscellaneous

```
"distribution: redhat"
"distribution: ubuntu"
"distribution_version: 20.04"
"distribution_version: 22.04"
"distribution_version: 8.6"
"distribution_version: 8.7"
"distribution_version: 9.2"
"distribution_major_version: 20"
"distribution_major_version: 22"
"distribution_major_version: 8"
"distribution_major_version: 9"
```

## CentOS Stream 9

```
"os_family: redhat"
"distribution: centos"
"distribution_major_version: 9"
"distribution_release: stream"
"distribution_version: 9"
```

## Miscellaneous Linux

```
"ks-rhel8: distribution_major_version: 8"
"ks-rhel8: distribution: redhat"
"ks-rhel8: distribution_release: ootpa"
"ks-rhel8: distribution_version: 8.8"
"ks-rhel8: os_family: redhat"
"ks-rhel9: distribution_major_version: 9"
"ks-rhel9: distribution: redhat"
"ks-rhel9: distribution_release: plow"
"ks-rhel9: distribution_version: 9.3"
"ks-rhel9: os_family: redhat"
"lab-test1: distribution: centos"
"lab-test1: distribution_major_version: 9"
"lab-test1: distribution_release: stream"
"lab-test1: distribution_version: 9"
"lab-test1: os_family: redhat"
"localhost: distribution_major_version: 23"
"localhost: distribution_release: mantic"
"localhost: distribution: ubuntu"
"localhost: distribution_version: 23.10"
"localhost: os_family: debian"
"tmp-moosa1: distribution_major_version: 22"
"tmp-moosa1: distribution_release: jammy"
"tmp-moosa1: distribution: ubuntu"
"tmp-moosa1: distribution_version: 22.04"
"tmp-moosa1: os_family: debian"
"zazu: distribution: fedora"
"zazu: distribution_major_version: 40"
"zazu: distribution_release: "
"zazu: distribution_version: 40"
"zazu: os_family: redhat"
```

## Oracle Linux 7

```
# "os_family: RedHat"
# "distribution: OracleLinux"
# "distribution_file_variety: OracleLinux"
# "distribution_release: NA"
# "distribution_major_version: 7"
```

## Virtualization examples

Inside podman container:

```
"ansible_virtualization_role": "guest",
"ansible_virtualization_tech_guest": [
 	"container",
 	"podman"
],
"ansible_virtualization_tech_host": [
 	"kvm"
],
"ansible_virtualization_type": "podman",
```

Linux bare metal host with KVM installed:

```
"ansible_virtualization_role": "host",
"ansible_virtualization_tech_guest": [],
"ansible_virtualization_tech_host": [
 	"kvm"
],
"ansible_virtualization_type": "kvm",
```

Proxmox host:

```
"ansible_virtualization_role": "host",
"ansible_virtualization_tech_guest": [],
"ansible_virtualization_tech_host": [
 	"kvm"
],
"ansible_virtualization_type": "kvm",
```

KVM guest:

```
"ansible_virtualization_role": "guest",
"ansible_virtualization_tech_guest": [
 	"kvm"
],
"ansible_virtualization_tech_host": [
 	"kvm"
],
"ansible_virtualization_type": "kvm",
```

KubeVirt VM:

```
molecule-centos9: virtualization_role: guest
molecule-centos9: virtualization_type: kubevirt
```

## macOS:

```
"system: darwin"
"os_family: darwin"
"distribution: macosx"
"distribution_major_version: 15"
"distribution_release: 24.2.0"
"distribution_version: 15.2"
"virtualization_role: "
"virtualization_type: "
```
