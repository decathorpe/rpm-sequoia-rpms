# work-in-progress RPM packages for rpm-sequoia

### Steps to build:

- modify .spec file
- build SRPM file: `rpmbuild -bs rust-rpm-sequoia.spec`
- build RPM files: `mock -r fedora-rawhide-x86_64 ./*.src.rpm`

### TODO:

- unversioned .so file in `%{_libdir}` is forbidden
- fix `License` tag to reflect statically linked dependencies
