# 第2回：Pythonでの構造化とモジュール分割

この回では、C言語と比較しながらPythonらしいモジュール分割を学びます。

## 学習内容

### ① C言語とPythonの設計スタイルの違い

- ヘッダファイルとモジュールの役割を対比
- Pythonではimportによる再利用が容易

> [!TIP]
>
> - Cでのファイル構成とPythonパッケージを並べてみよう
> - どちらが保守しやすいかを議論してみる

### ② ファイル分割とimportの基本

- 複数ファイルに分けて機能を整理
- `from package import module` の使い方

### ③ データと処理の分離

- 設定値はconfig、処理はlogicというように責務を区別
- グローバル変数を減らしてテストしやすくする

### ④ config、logic、interfaceの責務

- 役割を明示するとコードを追いやすい
- モジュール内での命名規則も決めておく

### ⑤ まとめと次回予告

- 構造化によって見通しが良くなる
- 次回：クラスとインスタンスでさらに整理する方法を学ぶ

## 追加解説

C言語と比較しながら、Pythonのモジュール設計を学ぶ回です。

- **C言語とPythonの違い**  
  Cではヘッダファイル(`.h`)で宣言し、実装ファイル(`.c`)で定義します。一方Pythonは`import`を使って関数やクラスを簡単に再利用できます。
- **ファイル分割・import**  
  `from package import module` などの基本的なimport文を整理し、複数ファイルに機能を分ける方法を確認。
- **データと処理の分離**  
  設定値用モジュールとロジック用モジュールを分け、責務を明確にします。

### 補足ポイント
- **C言語での例**
  ```c
  /* sensor.h */
  double read_temperature(void);

  /* sensor.c */
  #include "sensor.h"
  double read_temperature(void) {
      /* 実装 */
  }
  ```
  C言語ではヘッダと実装を分け、ビルド時にリンクする形式ですが、Pythonは下記のようにシンプルです。
- **Pythonでの例**
  ```python
  # sensor.py
  def read_temperature():
      # 実装
      return 25.0
  ```
  `import sensor` とするだけで関数を利用できる点を強調します。
