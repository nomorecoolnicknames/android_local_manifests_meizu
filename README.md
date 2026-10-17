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

- MX6 and M5c need `vendor/forge/ims` (IMS service), which is not public yet.
- The kernels are built from source. On the MX6 and the M5c boot images with the source-built kernels have been
  tested on the phones; on the M3 Note the configuration and device tree match the kernel running on the phone, but a
  boot image built this way has not been tested yet.
- The M3 Note OTA package checks the board before installing and accepts only the M681. A full `brunch` with the
  recovery and cache images and an installation on the phone have not been tested yet.
- The LineageOS platform changes these devices need are applied by `device/meizu/common` when
  `build/envsetup.sh` is sourced (see [its README](https://github.com/nomorecoolnicknames/android_device_meizu_common)).
- Google Camera on the MX6 is optional: run `device/meizu/m95/gcam/fetch-gcam.sh` and build with `M95_WITH_GCAM=true`.
