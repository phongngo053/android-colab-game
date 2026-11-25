# 📱 Host game mobile trên Google Colab / Kaggle

Chạy **Android thật** trong notebook, điều khiển từ điện thoại qua trình duyệt.

## 🚀 Mở trên Colab

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/phongngo053/android-colab-game/blob/main/colab-android-game.ipynb)

Trên Kaggle: vào <https://www.kaggle.com/code> → **Add New → Import Notebook / From URL** → dán link:

```
https://raw.githubusercontent.com/phongngo053/android-colab-game/main/colab-android-game.ipynb
```

> Kaggle chỉ nhận link dạng `raw.githubusercontent.com` (không phải link `blob`).

## Cách chạy

1. **CELL 1** — kiểm tra môi trường (có `/dev/kvm` không).
2. **CELL 2** — cài `adb` + `qemu`.
3. **CELL 3** — boot Android (chờ tới khi in `BOOT_OK`).
4. **CELL 4** — dựng web controller để điều khiển từ điện thoại.
5. **CELL 5** — in URL, mở URL đó bằng điện thoại.
6. **CELL 6** — tiện ích cài APK.

## Hai chế độ

| | Có `/dev/kvm` | Không `/dev/kvm` (Kaggle, Colab free) |
|---|---|---|
| Công cụ | Android Emulator (chính chủ) | QEMU + `android-x86_64` ISO |
| Ảnh | **Google Play** (API 30) → có Play Store | AOSP → **không có Play Store**, cài APK tay |
| Tốc độ | gần thật | mô phỏng mềm, chậm ~10-20 lần |

## ⚠️ Giới hạn thật

- Colab/Kaggle **cắt session khi không hoạt động** (~90 phút idle), tối đa ~12h.
- GPU của Colab (T4) **không** dùng được cho Android — Android trong QEMU vẽ bằng software renderer.
- Phù hợp: game 2D nhẹ, game pixel, test app, chụp màn hình, dịch game.
- Không hợp: game 3D nặng (Liên Minh, Genshin, PUBG) — cần VPS có KVM hoặc máy Android thật.

## Nguồn tải đã kiểm chứng

| Tệp | Nguồn | Kích thước |
|---|---|---|
| `platform-tools` (adb) | `dl.google.com/android/repository/platform-tools-latest-linux.zip` | 9.5 MB |
| Android Emulator (kèm QEMU) | `dl.google.com/android/repository/emulator-linux_x64-16982698.zip` | 353 MB |
| cmdline-tools | `dl.google.com/android/repository/commandlinetools-linux-11076708_latest.zip` | 153 MB |
| `android-x86_64-9.0-r2.iso` | HuggingFace `sdafsdaf/android_x86_images` (đã xác minh magic `CD001`) | 965 MB |

## Cấu trúc notebook

```
colab-android-game.ipynb
├── CELL 1  Kiểm tra môi trường (KVM?)
├── CELL 2  Cài adb + QEMU
├── CELL 3  Boot Android
├── CELL 4  Web controller (màn hình + tap + swipe + phím)
├── CELL 5  Expose cổng + tunnel dự phòng
└── CELL 6  Cài APK
```
