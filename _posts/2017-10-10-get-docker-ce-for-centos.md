# Prerequisites
## OS requirements

To install Docker CE, you need a maintained version of CentOS 7. Archive[归档] version aren't supported or tested.  

The centos-extras repository must be enabled. This repository is enabled by default, but if you have disabled it, you need to [re-enable](https://wiki.centos.org/AdditionalResources/Repositories) it.

## Uninstall old versions
Older versions of Docker were called docker or docker-engine. If these are installed, uninstall them, along with associated dependencies.  

    $ sudo yum remove docker \
                      docker-common \
                      docker-selinux \
                      docker-engine

It's OK if yum reports that none of these packages are installed.  

The content of /var/lib/docker/, including images, containers, volumns, and nerworks, are preserverd. Thw Docker CE package is now called docker-ce.

# Install Docker CE

You can install Docker CE in dfferent waus, depending on your needs:
- Most users set up Docker's repositories and install from them, for ease of installation and upgrade tasks. This is the recommended approach.

- Some users download the RPM package and install it manually and manage updgrades completely manually. This is useful in situations such as installing Docker on air-grapped systems with no access to the  internet.
- In testing and development environments, some users choose to use automated convenience[方便] scripts to install Docker.

## Install using the repository

Before you install Docker CE for first time on a new host machine, you need to set up the Docker repository. Afterward, you can install and update Docker from the repository.

### SET UP THE REPOSITORY

1. Install required packages. yum-utils provides the yum-config-manager utility, and lvm2 are required by the devicemapper storage driver.  

       $ sudo yum install -y yum-utils \
         device-mapper-persistent-data \
         lvm2

2. Use the following command to set up the stable repository. You always need the stable repository, even if you want to install builds from edge or test repositories as well.

       $ sudo yum-config-manager \
        --add-repo \
        https://download.docker.com/linux/centos/docker-ce.repo


3. Optional: Enable the edge and test repositories. These repositories are included in the docker.repo file above but are disables by default. You can enable them alongside the stable repository.

       $ sudo yum-config-manager --enable docker-ce-edge docker-ce-test

    You can disable the edge or test repository by running the yum-config-manager command with the --disable flag.

### INSTALL DOCKER CE

1. Install the lastest version of Docker CE, or go to the next step to install a specific version.

       $ sudo yum install docker-ce

2. On production system, you should install a specific version of Docker CE instead of always using the latest.

       $ yum list docker-ce --showduplicates | sort -r

    The version string is the package name plus the version up to[直到] the first hyphen[连字符]

3. Start Docker.

       $ sudo systemctl start docker

4. Verify that docker is installed correctly by running the hello-world image.

       $ sudo docker run hello-world