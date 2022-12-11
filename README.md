# TOPPERS/ASP3 体験キット

TOPPERS/ASP3 体験用に作成されたコンテナ内で、 TOPPERS/ASP3 のサンプルプログラム開発を体験できます。

## 体験手順

### サンプルプログラムの作成

```sh
# サンプルプログラム用ディレクトリの作成
mkdir /workspaces/toppers-asp3/mysample

# ASP3 に付属のサンプルビルド用ファイルをを作成
cd /workspaces/toppers-asp3/mysample
ruby ../configure.rb -T zybo_z7_gcc

# サンプルプログラムのビルド
make
```

### QEMU によるサンプルプログラムの実行

```sh
qemu-system-aarch64 -M arm-generic-fdt-7series -dtb /var/dts/zynq-zybo.dtb -serial null -serial mon:stdio -nographic -kernel ./asp
```

### GDB によるデバッグ実行

#### QEMU 実行用ターミナルを起動して QEMU を GDB 接続待ちで実行

```sh
cd /workspaces/toppers-asp3/mysample
qemu-system-aarch64 -M arm-generic-fdt-7series -dtb /var/dts/zynq-zybo.dtb -serial null -serial mon:stdio -nographic -kernel ./asp -s -S
```

#### GDB 実行用ターミナルを起動して、 GDB を起動

```sh
gdb-multiarch -q ./asp -ex "target remote localhost:1234"
```

# TODO

- `toppers-asp3` のディレクトリとアプリのディレクトリを別々にしたい。
    - `toppers-asp3` 内に `mysample` がある構成ではなく、`toppers-asp3` と `mysample` が隣同士にある構成にしたい
