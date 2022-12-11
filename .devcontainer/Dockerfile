FROM mikoto2000/qemu-xilinx:2021.1 AS qemu
FROM mikoto2000/che-toppers-kernel-build-kit:dev

USER root

# build-env から必要なファイルをコピー
# `/usr/local/bin/qemu-system-aarch64` をコピー
COPY --from=qemu \
    /usr/local/bin/qemu-system-aarch64 \
    /usr/local/bin/qemu-system-aarch64

# `ldd /usr/local/bin/qemu-system-aarch64` で表示される
# ライブラリ群をインストール
RUN apt-get update \
    && apt-get -y install \
        libpixman-1-0 \
        libglib2.0-0 \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

COPY --from=qemu \
    /usr/local/share/qemu \
    /usr/local/share/qemu

COPY --from=qemu \
    /var/dts \
    /var/dts

# gdb-multiarch をインストール
RUN apt-get update && apt-get -y install --no-install-recommends \
    gdb-multiarch \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

USER user

