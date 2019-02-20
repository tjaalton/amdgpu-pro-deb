# amdgpu-pro-deb
A packaging wrapper to allow pushing the amdgpu-pro deb's to an APT archive

This wrapper allows taking the tarball from AMD, and turn it into a source package which can be uploaded to an archive.
Building this source package unpacks the upstream deb's and then repacks them after doing some minor modifications to
the control data (like, setting the source package etc) required by the apt archive. Package contents are not touched.

The steps to create the package are:

- first run prep-pkg
# debian/prep-pkg ../amdgpu-pro-....tar.xz

- then either build locally
# fakeroot debian/rules binary

- or build the source package
# debian/rules gentarball
# dpkg-buildpackage -S -d -sa -I -i

- and push the source to a ppa

NOTE: the EULA still prohibits distributing the result:

>>>
3. RESTRICTIONS

Except for the limited license expressly granted in Section 2 herein, You have no other rights in the 
Software, whether express, implied, arising by estoppel or otherwise. Further restrictions regarding Your 
use of the Software are set forth below. You may not:

  1. modify or create derivative works of the Software;
  2. distribute, assign or otherwise transfer the Software;
...
<<<
