[![NKN](https://github.com/nknorg/nkn/wiki/img/nkn_logo.png)](https://nkn.org)

# NKN: a Scalable Self-Evolving and Self-Incentivized Decentralized Network

> NKN, short for New Kind of Network, is a project aiming to rebuild the
> Internet that will be truly open, decentralized, dynamic, safe, shared and
> owned by the community.

Official website: [https://nkn.org/](https://nkn.org/)

## Introduction

The core of the NKN network consists of many connected nodes distributed
globally. Every node is only connected to and aware of a few other nodes called
neighbors. Packets can be transmitted from any node to any other node in an
efficient and verifiable route. Data can be sent to any clients without public
or static IP address using their permanent NKN address with end-to-end
encryption.

The relay workload can be verified using our Proof of Relay (PoR) algorithm. A
small and fixed portion of the packets will be randomly selected as proof. The
random selection can be verified and cannot be predicted or controlled. Proof
will be sent to other nodes for payment and rewards.

A node in our network is both relayer and consensus participant. Consensus among
massive nodes can be reached efficiently by only communicating with neighbors
using our consensus algorithm based on Cellular Automata. Consensus is reached
for every block to prevent fork.

More details can be found in [our wiki](https://github.com/nknorg/nkn/wiki).

## Technical Highlights

* Transmit any data to any node/client without any centralized server
* Proof-of-Relay, a useful proof of work: mining is relaying data
* Extremely scalable consensus algorithm (millions or even billions of nodes)
* Strong consistency rather than eventual consistency
* Dynamic, large-scale network
* Verifiable topology and routes

## Building

The requirements to build are:
* Go version 1.8 or later
* Properly configured Go environment

Create directory $GOPATH/src/github.com/nknorg/ if not exists

In directory $GOPATH/src/github.com/nknorg/ clone the repository

```shell
$ git clone https://github.com/nknorg/nkn.git
```

Build the source code with make

```shell
$ cd nkn
$ make glide
$ make vendor
$ make all
```

After building the source code, you should see two executable
programs:

* `nknd`: the nkn program
* `nknc`: command line tool for nkn control

## Deployment

**Note: this repository is in the early development stage and may not
have all functions working properly. It should be used only for testing
now.**

Create several directories to save exectuable files `nknd` `nknc` and
config file `config.json`.

``` shell
$ tree
.
├── n1
│   ├── config.json
│   ├── nknd
│   └── nknc
├── n2
│   ├── config.json
│   ├── nknd
│   └── nknc
├── n3
│   ├── config.json
│   ├── nknd
│   └── nknc
├── n4
│   ├── config.json
│   ├── nknd
│   └── nknc
├── ...
```

Create new wallet in each directory

``` shell
$ ./nknc wallet -c
Password:
Re-enter Password:
Address                            Public Key
-------                            ----------
AbgUvnaiDYbwmKEwSH532W3LPB8Ma2aYYx 0306dd2db26e3cfde2dbe5c8a17ea7c27f13f99c19e2cb59bc13e2d0c41589c7f1
```

Config the same bootstrap node address and public key to each
`config.json` file, for example:

```shell
{
  "Magic": 99281,
  "Version": 1,
  "ChordPort": 30000,
  "NodePort": 30001,
  "HttpWsPort": 30002,
  "HttpRestPort": 30003,
  "HttpJsonPort": 30004,
  "LogLevel": 1,
  "IsTLS": false,
  "ConsensusType": "ising",
  "SeedList": [
    "127.0.0.1:30000"
  ],
  "GenesisBlockProposer": [
    "0306dd2db26e3cfde2dbe5c8a17ea7c27f13f99c19e2cb59bc13e2d0c41589c7f1"
  ]
}
```

Note that ports in different `config.json` does not need to be different,
conflict in ports will be resolved automatically.

Start bootstrap node by creating a network

```shell
$ ./nknd -test create
Password:
```

Start other nodes by joining the network

```shell
$ ./nknd -test join
Password:
```

When the network contains enough nodes (usually 8+), stop the node that created
the network in order for the relay service to work properly. Nodes joining the
network later should use a live node as seed.

## Contributing

Can I contribute patches to NKN project?

Yes! Please open a pull request with signed-off commits. We appreciate
your help!

Please follow our [Golang Style Guide](https://github.com/nknorg/nkn/wiki/NKN-Golang-Style-Guide)
for coding style.

Please sign off your commit. If you don't sign off your patches, we
will not accept them. This means adding a line that says
"Signed-off-by: Name <email>" at the end of each commit, indicating
that you wrote the code and have the right to pass it on as an open
source patch. This can be done automatically by adding -s when
committing:

```shell
git commit -s
```

## Community

* [Telegram](https://t.me/nknorg)
* [Reddit](https://www.reddit.com/r/nknblockchain/)
* [Twitter](https://twitter.com/NKN_ORG)
* [Facebook](https://www.facebook.com/nkn.org)
