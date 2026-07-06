# i.MX Repo Manifest README

This repository is used to download manifests for Cargt's i.MX BSP releases.

---

## Install the `repo` utility

To use this manifest repo, the `repo` tool must be installed first:

```sh
mkdir ~/bin
curl http://commondatastorage.googleapis.com/git-repo-downloads/repo  > ~/bin/repo
chmod a+x ~/bin/repo
PATH=${PATH}:~/bin
```

---

## Install essential host packages

Your build host must install required packages for the Yocto build. Reference the section "Build Host Packages" in the document "Yocto Project Quick build":

- https://docs.yoctoproject.org/6.0/brief-yoctoprojectqs/index.html#build-host-packages

---

## Download the Yocto Project BSP

```sh
mkdir <release>
cd <release>
repo init -u https://github.com/cargt/imx_manifest -b wrynose -m cargt-imx-6.18.20-2.0.0.xml
repo sync
```

---

## Examples

To download this release (6.18.20-2.0.0):

```sh
repo init -u https://github.com/cargt/imx_manifest -b wrynose -m cargt-imx-6.18.20-2.0.0.xml
```

---

## Setup the build folder for a BSP release

```sh
[MACHINE=<machine>] [DISTRO=cargt-imx-<backend>] source ./imx-setup-release.sh -b bld-<backend>

<machine>   defaults to `imx93-cargt-00363-00365`
<backend>   Graphics backend type
    xwayland    Wayland with X11 support - default distro
    wayland     Wayland
    fb          Framebuffer (not supported for mx8)
```

Note: If the poky community distro is used, then build breaks will happen with some components using our `meta-imx` layer.

### Example: Setup for XWayland

```sh
MACHINE=imx93-cargt-00363-00365 DISTRO=cargt-imx-xwayland source ./imx-cargt-setup-release.sh -b bld-xwayland
```

---

## Build an image

```sh
bitbake <image recipe>
```

Some image recipes:

| Recipe               | Description                                      |
|----------------------|--------------------------------------------------|
| cargt-image-core     | core image with basic graphics and no multimedia |
| cargt-image-dev      | recommended development image                    |
| cargt-image-chrome   | image with chromium-ozone-wayland browser        |
| cargt-image-demo     | image with chromium browswer and NXP demo apps   |

---

## Additional Links

- [imx-manifest GitHub](https://github.com/nxp-imx/imx-manifest)
- [Pull requests](https://github.com/nxp-imx/imx-manifest/pulls)
- [Security](https://github.com/nxp-imx/imx-manifest/security)
- [Insights](https://github.com/nxp-imx/imx-manifest/pulse)
