# 第5回：責務分離とSOLID原則入門

この回では、保守性を高める設計原則としてSOLIDの要素を取り上げます。

## 学習内容

### ① 単一責任の原則（SRP）

- 1クラス1役割の考え方
- 責務が混在するとテストしにくい例

### ② 依存性逆転の感覚（DIP）

- 実装ではなく抽象に依存させる
- インターフェース越しの結合を体験

> [!TIP]
>
> - 既存コードから責務を抽出してみよう
> - 依存関係が減ると何がうれしいか話し合う

### ③ ファイル分割によるリファクタ演習

- 1ファイルに詰め込まれたクラスを分割
- テストしやすい構造に整理

### ④ まとめと次回予告

- 原則を知ると設計判断がブレにくくなる
- 次回：アーキテクチャパターンで全体構造を学ぶ

## 追加解説

SOLID原則のうち、単一責任の原則（SRP）と依存性逆転（DIP）を中心に取り上げます。

- **単一責任の原則（SRP）**  
  1クラス1役割を意識し、責務が混在しないように設計します。
- **依存性逆転の感覚（DIP）**  
  実装詳細に依存するのではなく、抽象（インターフェース）に依存させる設計を体験します。
- **ファイル分割によるリファクタ**  
  大きくなったファイルを責務ごとに分け、テストしやすい構造に整理します。

### 補足ポイント
- **依存性逆転の簡単な例**
  ```python
  from abc import ABC, abstractmethod

  class Database(ABC):
      @abstractmethod
      def save(self, data: str) -> None:
          pass

  class FileDatabase(Database):
      def save(self, data: str) -> None:
          with open('out.txt', 'w') as f:
              f.write(data)

  class Service:
      def __init__(self, db: Database):
          self.db = db

      def run(self):
          self.db.save('hello')
  ```
  `Service`は抽象`Database`に依存しているため、`FileDatabase`以外の実装に簡単に差し替え可能です。
