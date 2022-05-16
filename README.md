# work-in-progress RPM packages for rpm-sequoia

### Steps to build:

- `dnf install -y rpm-build mock`
- Get the latest version:
  `curl -L https://crates.io/api/v1/crates/rpm-sequoia/0.2.0/download --output rpm-sequoia-0.2.0.crate`
- Update .spec file as needed
- `mkdir -p ~/rpmbuild/SOURCES`
- `cp rpm-sequoia-0.2.0.crate ~/rpmbuild/SOURCES`
- build SRPM file: `rpmbuild -bs rust-rpm-sequoia.spec`
- We need to install [`cdylib-link-lines`](https://github.com/nwalfield/rpm-cdylib-link-lines):

```
mock -r fedora-rawhide-x86_64 ~/rpmbuild/SRPMS/rust-cdylib-link-lines-0.1.4-1.fc36.src.rpm \
  && mock -r fedora-rawhide-x86_64 -i /var/lib/mock/fedora-rawhide-x86_64/result/rust-cdylib-link-lines-devel-0.1.4-1.fc37.noarch.rpm \
  && mock -r fedora-rawhide-x86_64 -i /var/lib/mock/fedora-rawhide-x86_64/result/rust-cdylib-link-lines+default-devel-0.1.4-1.fc37.noarch.rpm
```
- build RPM files: `mock --no-clean -r fedora-rawhide-x86_64 ~/rpmbuild/SRPMS/rust-rpm-sequoia-*.src.rpm`

### TODO:

- fix `License` tag to reflect statically linked dependencies
