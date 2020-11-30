# juman++ & normalizeNumexp

## 1. juman++

https://qiita.com/Gushi_maru/items/ee434b5bc9f020c8feb6

## 2. normalizeNumexp

+ python2のインストール

```
sudo apt-get install python3
```

+ python リンクづくり

初期状態の場合にpythonコマンドがないからリンクを作る

```
cd /bin
sudo ln -s python2.7 python
```

+ インストールフォルダづくり

```
cd
mkdir normalizeNumexp_install
cd normalizeNumexp_install
```

+ uxをインストール

```
wget https://storage.googleapis.com/google-code-archive-downloads/v2/code.google.com/ux-trie/ux-0.1.9.tar.bz2
tar xvjf ux-0.1.9.tar.bz2
cd ux-0.1.9/
sudo ./waf configure
sudo ./waf build
sudo ./waf install
```

エラー（warning）が出る場合は直そう

‘class std::bad_alloc’が出てくる。「メモリ確保に失敗したで」らしい。どうすればええねん

無視してビルドするとlibux.soがねえぞって怒られる

```
ux: error while loading shared libraries: libux.so: cannot open shared object file: No such file or directory
```

結論：気にすんな

共有ライブラリに登録（パス通し）してあげる

```
sudo nano /etc/ld.so.conf
```

「~/normalizeNumexp_install/ux-0.1.9/build/src/libux.so」を追記して保存

```
sudo ldconfig
```

これでuxが起動するはず

```
$ ux
usage: ux --index=string [options] ...
options:
  -k, --keylist       key list (string [=])
  -i, --index         index (string)
  -l, --limit         limit at search (int [=10])
  -u, --uncompress    tail is uncompressed
  -e, --enumerate     enumerate all keywords
  -v, --verbose       verbose mode (int [=0])
  -h, --help          this message
```

+ pficommonをインストール

```
cd ..
git clone https://github.com/pfi/pficommon.git
cd pficommon
./waf configure
./waf
sudo ./waf install
```

怪しい...

```
Checking for header msgpack.hpp          : not found
Checking for header fcgiapp.h            : not found
Checking for header stdint.h             : yes
Checking for ''                          : not found
```

+ normalizeNumexpをインストール

```
cd ..
git clone https://github.com/nullnull/normalizeNumexp.git
cd normalizeNumexp
./waf configure
./waf 
sudo ./waf install
```

おけけ

