# xebecj

> A Java library for working with Xebec

[![Build Status](https://travis-ci.com/xebecproject/xebecj.svg?token=Pzix7aqnMuGS9c6BmBz2&branch=master)](https://travis-ci.com/xebecproject/xebecj)

### Welcome to xebecj

The xebecj library is a Java implementation of the Xebec protocol, which allows it to maintain a wallet and send/receive transactions without needing a local copy of Xebec Core. It comes with full documentation and some example apps showing how to use it.

### Technologies

* Java 6 for the core modules, Java 8 for everything else
* [Maven 3+](http://maven.apache.org) - for building the project
* [Google Protocol Buffers](https://github.com/google/protobuf) - for use with serialization and hardware communications

### Getting started

To get started, it is best to have the latest JDK and Maven installed. The HEAD of the `master` branch contains the latest development code and various production releases are provided on feature branches.

#### Building from the command line
To initialize the repo after cloning it: 
```
git submodule update  --init --recursive
```
To perform a full build use (this includes the xebecjbls shared library):
```
mvn clean package
```
To perform a full build without building the bls shared library and skip the test:
```
mvn clean package -Pno-build-bls -DskipTests
```
To perform a full build and install it in the local maven repository:
```
mvn clean install
```
You can also run
```
mvn site:site
```
to generate a website with useful information like JavaDocs.

The outputs are under the `target` directory.

#### Building from an IDE

Alternatively, just import the project using your IDE. [IntelliJ](http://www.jetbrains.com/idea/download/) has Maven integration built-in and has a free Community Edition. Simply use `File | Import Project` and locate the `pom.xml` in the root of the cloned project source tree.

The xebecjbls library must still be built with `mvn`.

### Example applications

These are found in the `examples` module.

#### Forwarding service

This will download the block chain and eventually print a Xebec address that it has generated.

If you send coins to that address, it will forward them on to the address you specified.

```
  cd examples
  mvn exec:java -Dexec.mainClass=org.xebecj.examples.ForwardingService -Dexec.args="<insert a xebec address here>"
```

Note that this example app *does not use checkpointing*, so the initial chain sync will be pretty slow. You can make an app that starts up and does the initial sync much faster by including a checkpoints file; see the documentation for
more info on this technique.
