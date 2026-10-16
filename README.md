# Local manifests for Meizu devices

[repo](https://gerrit.googlesource.com/git-repo) local manifests for LineageOS 20.0.

| File | Device |
| --- | --- |
| `meizu_m95.xml` | Meizu MX6 (m95, MT6797) |
| `meizu_m5c.xml` | Meizu M5c (m5c, MT6737M) |
| `meizu_m3note.xml` | Meizu M3 Note (M681 / L681, MT6755) |

```sh
repo init -u https://github.com/LineageOS/android.git -b lineage-20.0 --git-lfs
mkdir -p .repo/local_manifests
curl -L -o .repo/local_manifests/meizu_m95.xml \
  https://raw.githubusercontent.com/nomorecoolnicknames/android_local_manifests_meizu/lineage-20.0/meizu_m95.xml
repo sync -c
source build/envsetup.sh
breakfast m95
brunch m95
```

## Known gaps

These trees do not build a complete ROM yet:

- MX6 and M5c need `vendor/forge/ims` (IMS service), which is not public yet.
- The device trees still use prebuilt kernels; the MX6 one is missing some stock configuration files.
- The LineageOS platform changes these devices need are applied by `device/meizu/common` when
  `build/envsetup.sh` is sourced (see [its README](https://github.com/nomorecoolnicknames/android_device_meizu_common));
  they are being moved into the device trees.
