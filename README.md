[![Linux Build Status](https://travis-ci.org/containernetworking/cni.svg?branch=master)](https://travis-ci.org/containernetworking/cni)
[![Windows Build Status](https://ci.appveyor.com/api/projects/status/wtrkou8oow7x533e/branch/master?svg=true)](https://ci.appveyor.com/project/cni-bot/cni/branch/master)
[![Coverage Status](https://coveralls.io/repos/github/containernetworking/cni/badge.svg?branch=master)](https://coveralls.io/github/containernetworking/cni?branch=master)
[![Slack Status](https://cryptic-tundra-43194.herokuapp.com/badge.svg)](https://cryptic-tundra-43194.herokuapp.com/)

![CNI Logo](logo.png)

---

# Community Sync Meeting

There is a community sync meeting for users and developers every 1-2 months. The next meeting will be held on a Google Hangout and the link is in the [agenda](https://docs.google.com/document/d/10ECyT2mBGewsJUcmYmS8QNo1AcNgy2ZIe2xS7lShYhE/edit?usp=sharing) (Notes from previous meeting are also in this doc).

The next meeting will be held on *Wednesday, January 30th, 2019* at *4:00pm UTC / 11:00am EDT / 8:00am PDT* [Add to Calendar](https://www.worldtimebuddy.com/?qm=1&lid=100,5,2643743,5391959&h=100&date=2019-01-30&sln=16-17).

---

# CNI - the Container Network Interface

## What is CNI?

CNI (_Container Network Interface_), a [Cloud Native Computing Foundation](https://cncf.io) project, consists of a specification and libraries for writing plugins to configure network interfaces in Linux containers, along with a number of supported plugins.
CNI concerns itself only with network connectivity of containers and removing allocated resources when the container is deleted.
Because of this focus, CNI has a wide range of support and the specification is simple to implement.

As well as the [specification](SPEC.md), this repository contains the Go source code of a [library for integrating CNI into applications](libcni) and an [example command-line tool](cnitool) for executing CNI plugins.  A [separate repository contains reference plugins](https://github.com/containernetworking/plugins) and a template for making new plugins.

The template code makes it straight-forward to create a CNI plugin for an existing container networking project.
CNI also makes a good framework for creating a new container networking project from scratch.

## Why develop CNI?

Application containers on Linux are a rapidly evolving area, and within this area networking is not well addressed as it is highly environment-specific.
We believe that many container runtimes and orchestrators will seek to solve the same problem of making the network layer pluggable.

To avoid duplication, we think it is prudent to define a common interface between the network plugins and container execution: hence we put forward this specification, along with libraries for Go and a set of plugins.

## Who is using CNI?
### Container runtimes
- [rkt - container engine](https://coreos.com/blog/rkt-cni-networking.html)
- [Kubernetes - a system to simplify container operations](https://kubernetes.io/docs/admin/network-plugins/)
- [OpenShift - Kubernetes with additional enterprise features](https://github.com/openshift/origin/blob/master/docs/openshift_networking_requirements.md)
- [Cloud Foundry - a platform for cloud applications](https://github.com/cloudfoundry-incubator/cf-networking-release)
- [Apache Mesos - a distributed systems kernel](https://github.com/apache/mesos/blob/master/docs/cni.md) ** beware all versions [do not](https://issues.apache.org/jira/browse/MESOS-7178) support cni spec [0.3.0](https://github.com/containernetworking/cni/blob/spec-v0.3.0/SPEC.md) **
- [Amazon ECS - a highly scalable, high performance container management service](https://aws.amazon.com/ecs/)
- [Singularity - container platform optimized for HPC, EPC, and AI](https://github.com/sylabs/singularity)
- [OpenSVC - orchestrator for legacy and containerized application stacks](https://docs.opensvc.com/latest/fr/agent.configure.cni.html)

### 3rd party plugins
- [Project Calico - a layer 3 virtual network](https://github.com/projectcalico/calico-cni)
- [Weave - a multi-host Docker network](https://github.com/weaveworks/weave)
- [Contiv Networking - policy networking for various use cases](https://github.com/contiv/netplugin)
- [SR-IOV](https://github.com/hustcat/sriov-cni)
- [Cilium - BPF & XDP for containers](https://github.com/cilium/cilium)
- [Infoblox - enterprise IP address management for containers](https://github.com/infobloxopen/cni-infoblox)
- [Multus - a Multi plugin](https://github.com/Intel-Corp/multus-cni)
- [Romana - Layer 3 CNI plugin supporting network policy for Kubernetes](https://github.com/romana/kube)
- [CNI-Genie - generic CNI network plugin](https://github.com/Huawei-PaaS/CNI-Genie)
- [Nuage CNI - Nuage Networks SDN plugin for network policy kubernetes support ](https://github.com/nuagenetworks/nuage-cni)
- [Silk - a CNI plugin designed for Cloud Foundry](https://github.com/cloudfoundry-incubator/silk)
- [Linen - a CNI plugin designed for overlay networks with Open vSwitch and fit in SDN/OpenFlow network environment](https://github.com/John-Lin/linen-cni)
- [Vhostuser - a Dataplane network plugin - Supports OVS-DPDK & VPP](https://github.com/intel/vhost-user-net-plugin)
- [Amazon ECS CNI Plugins - a collection of CNI Plugins to configure containers with Amazon EC2 elastic network interfaces (ENIs)](https://github.com/aws/amazon-ecs-cni-plugins)
- [Bonding CNI - a Link aggregating plugin to address failover and high availability network](https://github.com/Intel-Corp/bond-cni)
- [ovn-kubernetes - an container network plugin built on Open vSwitch (OVS) and Open Virtual Networking (OVN) with support for both Linux and Windows](https://github.com/openvswitch/ovn-kubernetes)
- [Juniper Contrail](https://www.juniper.net/cloud) / [TungstenFabric](https://tungstenfabric.io) -  Provides overlay SDN solution, delivering multicloud networking, hybrid cloud networking, simultaneous overlay-underlay support, network policy enforcement, network isolation, service chaining and flexible load balancing
- [Knitter - a CNI plugin supporting multiple networking for Kubernetes](https://github.com/ZTE/Knitter)
- [DANM - a CNI-compliant networking solution for TelCo workloads running on Kubernetes](https://github.com/nokia/danm)
- [VMware NSX – a CNI plugin that enables automated NSX L2/L3 networking and L4/L7 Load Balancing; network isolation at the pod, node, and cluster level; and zero-trust security policy for your Kubernetes cluster.](https://docs.vmware.com/en/VMware-NSX-T/2.2/com.vmware.nsxt.ncp_kubernetes.doc/GUID-6AFA724E-BB62-4693-B95C-321E8DDEA7E1.html)
- [cni-route-override - a meta CNI plugin that override route information](https://github.com/redhat-nfvpe/cni-route-override)
- [Terway - a collection of CNI Plugins based on alibaba cloud VPC/ECS network product](https://github.com/AliyunContainerService/terway)

The CNI team also maintains some [core plugins in a separate repository](https://github.com/containernetworking/plugins).


## Contributing to CNI

We welcome contributions, including [bug reports](https://github.com/containernetworking/cni/issues), and code and documentation improvements.
If you intend to contribute to code or documentation, please read [CONTRIBUTING.md](CONTRIBUTING.md). Also see the [contact section](#contact) in this README.

## How do I use CNI?

### Requirements

The CNI spec is language agnostic.  To use the Go language libraries in this repository, you'll need a recent version of Go.  You can find the Go versions covered by our [automated tests](https://travis-ci.org/containernetworking/cni/builds) in [.travis.yaml](.travis.yml).

### Reference Plugins

The CNI project maintains a set of [reference plugins](https://github.com/containernetworking/plugins) that implement the CNI specification.
NOTE: the reference plugins used to live in this repository but have been split out into a [separate repository](https://github.com/containernetworking/plugins) as of May 2017.

### Running the plugins

After building and installing the [reference plugins](https://github.com/containernetworking/plugins), you can use the `priv-net-run.sh` and `docker-run.sh` scripts in the `scripts/` directory to exercise the plugins.

**note - priv-net-run.sh depends on `jq`**

Start out by creating a netconf file to describe a network:

```bash
$ mkdir -p /etc/cni/net.d
$ cat >/etc/cni/net.d/10-mynet.conf <<EOF
{
	"cniVersion": "0.2.0",
	"name": "mynet",
	"type": "bridge",
	"bridge": "cni0",
	"isGateway": true,
	"ipMasq": true,
	"ipam": {
		"type": "host-local",
		"subnet": "10.22.0.0/16",
		"routes": [
			{ "dst": "0.0.0.0/0" }
		]
	}
}
EOF
$ cat >/etc/cni/net.d/99-loopback.conf <<EOF
{
	"cniVersion": "0.2.0",
	"name": "lo",
	"type": "loopback"
}
EOF
```

The directory `/etc/cni/net.d` is the default location in which the scripts will look for net configurations.

Next, build the plugins:

```bash
$ cd $GOPATH/src/github.com/containernetworking/plugins
$ ./build_linux.sh # or build_windows.sh
```

Finally, execute a command (`ifconfig` in this example) in a private network namespace that has joined the `mynet` network:

```bash
$ CNI_PATH=$GOPATH/src/github.com/containernetworking/plugins/bin
$ cd $GOPATH/src/github.com/containernetworking/cni/scripts
$ sudo CNI_PATH=$CNI_PATH ./priv-net-run.sh ifconfig
eth0      Link encap:Ethernet  HWaddr f2:c2:6f:54:b8:2b  
          inet addr:10.22.0.2  Bcast:0.0.0.0  Mask:255.255.0.0
          inet6 addr: fe80::f0c2:6fff:fe54:b82b/64 Scope:Link
          UP BROADCAST MULTICAST  MTU:1500  Metric:1
          RX packets:1 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:1 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:90 (90.0 B)  TX bytes:0 (0.0 B)

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)
```

The environment variable `CNI_PATH` tells the scripts and library where to look for plugin executables.

## Running a Docker container with network namespace set up by CNI plugins

Use the instructions in the previous section to define a netconf and build the plugins.
Next, docker-run.sh script wraps `docker run`, to execute the plugins prior to entering the container:

```bash
$ CNI_PATH=$GOPATH/src/github.com/containernetworking/plugins/bin
$ cd $GOPATH/src/github.com/containernetworking/cni/scripts
$ sudo CNI_PATH=$CNI_PATH ./docker-run.sh --rm busybox:latest ifconfig
eth0      Link encap:Ethernet  HWaddr fa:60:70:aa:07:d1  
          inet addr:10.22.0.2  Bcast:0.0.0.0  Mask:255.255.0.0
          inet6 addr: fe80::f860:70ff:feaa:7d1/64 Scope:Link
          UP BROADCAST MULTICAST  MTU:1500  Metric:1
          RX packets:1 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:1 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:90 (90.0 B)  TX bytes:0 (0.0 B)

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)
```

## What might CNI do in the future?

CNI currently covers a wide range of needs for network configuration due to its simple model and API.
However, in the future CNI might want to branch out into other directions:

- Dynamic updates to existing network configuration
- Dynamic policies for network bandwidth and firewall rules

If these topics are of interest, please contact the team via the mailing list or IRC and find some like-minded people in the community to put a proposal together.

## Contact

For any questions about CNI, please reach out on the mailing list:
- Email: [cni-dev](https://groups.google.com/forum/#!forum/cni-dev)
- IRC: #[containernetworking](irc://irc.freenode.org:6667/#containernetworking) channel on freenode.org
- Slack: [containernetworking.slack.com](https://cryptic-tundra-43194.herokuapp.com)
