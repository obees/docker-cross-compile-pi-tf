# docker-cross-compile-pi-tf
Cross compile tensorflow for raspberry pi3

## get the github repo
```
> git clone https://github.com/obees/docker-cross-compile-pi-tf.git
> git checkout pi3
> cd docker-cross-compile-pi-tf.git
```

## launch docker
```
> docker run -v `pwd`:/install2 -it tensorflow/tensorflow:latest-devel-py3 bash
```

## run the commands inside the container 
```
> /install2/install_bootstrap_deb_packages.sh
```
```
> add-apt-repository -y ppa:openjdk-r/ppa && \
add-apt-repository -y ppa:george-edison55/cmake-3.x
```
```
> /install2/install_deb_packages.sh
```
```
> /install2/install_pip_packages.sh
```
```
> /install2/install_bazel.sh
```
```
> /install2/install_proto3.sh
```
```
> /install2/install_buildifier.sh
```
```
> /install2/install_auditwheel.sh
```
```
> /install2/install_golang.sh
```

## The following line installs the Python cross-compilation toolchain. All the
## preceding dependencies should be kept in sync with the main CPU docker file.
```
> /install2/install_pi_python3_toolchain.sh
```

## Set up the master bazelrc configuration file.
```
> install2/.bazelrc /etc/bazel.bazelrc
```

## Cross-compile
```
> /tensorflow/tensorflow/tools/ci_build/pi/build_raspberry_pi.sh
```

