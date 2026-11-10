# Device tree for the Xiaomi Redmi Pad SE (xun)

## Device specifications

| Basic                   | Spec                                                           |
| ----------------------- | :------------------------------------------------------------- |
| SoC                     | Qualcomm Snapdragon 680 (6nm)                                  |
| CPU                     | Octa-core (4x2.4 GHz Kryo 265 Gold & 4x1.9 GHz Kryo 265 Silver)|
| GPU                     | Adreno 610                                                     |
| Memory                  | 4/6/8GB                                                        |
| Shipped Android version | 13                                                             |
| Storage                 | 128/256GB                                                      |
| MicroSD                 | MicroSDXC                                                      |
| Battery                 | Non-removable Li-Po 8000 mAh                                   |
| Dimensions              | 255.5 x 167.1 x 7.4 mm                                         |
| Display                 | 1200 x 1920 pixels, 11 inches                                  |
| Rear Camera             | 8 MP, f/2.0, (wide), 1/4", 1.12µm, AF                          |
| Front Camera            | 5 MP, f/2.2, (ultrawide), 1/5", 1.12µm                         |

## Device Picture

![Xiaomi Redmi Pad SE](https://i02.appmifile.com/699_operator_sg/05/09/2023/0b581a06715510c656552d79ca19d62a.png?f=webp)

## Building LineageOS 24.0 (Android 17)

```bash
repo init -u https://github.com/LineageOS/android.git -b lineage-24.0 --git-lfs
git clone https://github.com/decoder-dev/local_manifests -b lineage-24.0 .repo/local_manifests
repo sync -c -j$(nproc --all) --force-sync --no-clone-bundle --no-tags
source build/envsetup.sh
breakfast xun
m bacon
```

[local_manifests](https://github.com/decoder-dev/local_manifests) lists every
repository the build needs on top of the LineageOS 24.0 manifest.

### Notes

- Bengal is a UM 4.19 platform for `hardware/qcom-caf/common`, but this
  device runs a 5.15 GKI kernel with the AudioReach audio stack.
  [hardware_qcom-caf_common](https://github.com/decoder-dev/hardware_qcom-caf_common)
  is the LineageOS repository plus one commit that selects the sm6225 HALs
  and the sm8550 vendor sepolicy for bengal when `TARGET_KERNEL_VERSION`
  is 5.15.
- The Xiaomi QTI sepolicy that used to come from a forked `hardware/xiaomi`
  lives in `sepolicy/`, so the official `hardware/xiaomi` is used.
- The sm6225 HALs and the prebuilt kernel come from
  [Xiaomi-Redmi-Pad-SE-Resources](https://github.com/Xiaomi-Redmi-Pad-SE-Resources),
  which has no lineage-24.0 branches yet, so their lineage-23.2 branches
  are used.
