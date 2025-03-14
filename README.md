# ACCESS-rAM3

## About the model

The ACCESS Regional Area Model (ACCESS-rAM) is an implementation of the [UK Met Office (UKMO)](https://www.metoffice.gov.uk/) regional nesting suite, comprising atmosphere and land components.
Unlike the UKMO regional nesting suite that relies on operational land-surface initial conditions, ACCESS-rAM derives its initial conditions from alternative sources, enhancing its capability for high-resolution regional atmosphere modelling.

For more information see the [ACCESS-Hive Docs model description](https://access-hive.org.au/models/configurations/access-ram/) and [how to run the model](https://access-hive.org.au/models/run-a-model/run-access-ram/).

## About this repository

This is the Model Deployment Repository for the ACCESS-rAM3 model. 

## Releases

Release information is available on the [ACCESS Hive Forum release topic](https://forum.access-hive.org.au/t/access-ram3-release-information/4308).



## Support

[ACCESS-NRI](https://www.access-nri.org.au) supports ACCESS-rAM3 for the Australian Research Community.

Any questions about ACCESS-NRI releases of ACCESS-rAM3 should be done through the [ACCESS-Hive Forum](https://forum.access-hive.org.au/). See the [ACCESS Help and Support topic](https://forum.access-hive.org.au/t/access-help-and-support/908) for details on how to do this.

### Build

ACCESS-NRI is using [spack](https://spack.io), a build from source package manager designed for use with high performance computing. This repository contains a [spack environment](https://spack.readthedocs.io/en/latest/environments.html) definition file ([`spack.yaml`](./spack.yaml)) that defines all the essential components of the model, including exact versions.

Spack automatically builds all the components and their dependencies, producing model component executables. Spack already contains support for compiling thousands of common software packages. Spack packages for the components are defined in the [spack packages repository](https://github.com/ACCESS-NRI/spack_packages/).

ACCESS-rAM3 is built and deployed automatically to `gadi` on NCI (see below). However it is possible to use spack to compile the model using the `spack.yaml` environment file in this repository. To do so follow the [instructions on for configuring spack on `gadi`]([https://forum.access-hive.org.au/t/how-to-build-access-om2-on-gadi/1545](https://access-hive.org.au/getting_started/spack/)).

Then clone this repository and run the following commands on `gadi`:

```bash
spack env create access-ram3 spack.yaml
spack env activate access-ram3
spack install
```

to create a spack environment called `access-ram3` and build all the components, the locations of which can be found using `spack find --paths`.

### Deployment

ACCESS-rAM3 is deployed automatically when a new version of the [`spack.yaml`](./spack.yaml) file is committed to `main` or a dedicated `backport/VERSION` branch. All the ACCESS-rAM3 components are built using `spack` on `gadi` and installed under the [`vk83`](https://my.nci.org.au/mancini/project/vk83) project in `/g/data/vk83`. It is necessary to be a member of [`vk83`](https://my.nci.org.au/mancini/project/vk83) project to use ACCESS-NRI deployments of ACCESS-OM2.

The deployment process also creates a GitHub release with the same tag. All releases are available under the [Releases page](https://github.com/ACCESS-NRI/ACCESS-rAM3/releases). Each release has a changelog and meta-data with detailed information about the build and deployment, including:

- paths on `gadi` to all executables built in the deployment process (`spack.location`)
- a `spack.lock` file, which is a complete build provenance document, listing all the components that were built and their dependencies, versions, compiler version, build flags and build architecture
- the environment `spack.yaml` file used for deployment

Additionally the deployment creates environment modulefiles, the [standard method for deploying software on `gadi`](https://opus.nci.org.au/display/Help/Environment+Modules). To view available ACCESS-rAM3 versions:

```bash
module use /g/data/vk83/modules
module avail access-ram3
```

For users of ACCESS-rAM3 model configurations released by ACCESS-NRI the exact location of the model executables is not required. Model configurations will be updated with new model components when necessary.

For information on contributing your own fixes to the ACCESS-rAM3 `spack.yaml`, see the [CONTRIBUTING.md](./CONTRIBUTING.md) file.

