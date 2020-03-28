lesson-compress

### tar.gz

#### ファイルの圧縮

```
import tarfile　

with tarfile.open('test.tar.gz', 'w:gz') as tr:
モード"w"だけだと"tar"を一まとめにするだけ。圧縮するには　:gz　をつける。
    tr.add('test_dir')

#test.tar.gzフォルダができる
```

#### python で展開する。

```
 with tarfile.open('test.tar.gz', 'r:gz') as tr:
 #読み込みをするのでモードは　"r"
    tr.extractall(path='test_dir')
#.extractall[指定ファイル全てを展開、解凍] path[展開先のディレクトリのパスを指定 = test_dir]

```

#### 一つずつ展開したファイルを確認する。

```
with tarfile.open('test.tar.gz', 'r:gz') as tr:
    # tr.extractall(path='test_dir')
    with tr.extractfile('test_dir/sub_dir/sub_test.txt') as f:
#extractfile[ファイルを一つずつ取る]（直訳：抽出ファイル）
#この場合sub_test.txtの中身を取ってくる。
        print(f.read())
#read()はファイルを全て読み込み、その文字列データに対して処理を行う。
#この場合は('test_dir/sub_dir/sub_test.txt')に対して処理、読み込みを行う
```

### zip

### zip ファイルの圧縮：作成

```
import zipfile

with zipfile.zipfile('test.zip', 'w') as z:
    z.write('test_dir')
#z.write('test_dir')だけだとフォルダしか作られない。

    z.write('test_dir/test.txt')
#z.write('test_dir/test.txt')自分で作りたいtxt名を入力する。

```

- unzip test.zip -d zzz をターミナルに打つことでファイルの確認ができる。

#### zip ファイルの展開

```
impot glob

with zipfile.ZipFile('test.zip', 'w') as z:

    for f in glob.glob('test_dir/**', recursive=True):
#test_dirの下にあるファイルをrecursive(直訳：再帰的)で見ていく。
#globは引数に指定されたパターンにマッチするファイルパス名を取得できる。
#*[アスタリスク]１つだとtest_dirと同じディレクトリまでしか見れない。
#**[アスタリスク]2つだと更に深く見ることができる。

        print(f)
        z.write(f)
#zipファイル


```

- zip ファイルの読み込み

```
with zipfile.ZipFile('test.zip', 'r') as z:
#"r"にする
    z.extractall('zzz2')
#ファイル名は'zzz2'にした。なんでもいい。

```

#### 一つずつ展開したファイルを確認する。

```
with zipfile.ZipFile('test.zip', 'r') as z:

    z.extractall('zzz2')
#extractfile[ファイルを一つずつ取る]（直訳：抽出ファイル）
#この場合zzz2の中身を取ってくる。

    with z.open('test_dir/test.txt') as f:

        print(f.read())
#read()はファイルを全て読み込み、その文字列データに対して処理を行う。
#この場合は('test_dir/test.txt')に対して処理、読み込みを行う
```
