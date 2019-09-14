# visual studio users community #1

## 今日からできる簡単.NET高速化tips

顧客に勝ち提供Wするのが最優先

高速化

- 最善手はボトルネック改善
- 実装でも変えられる

早いコードを書くという意識が必要

最速の開発環境・実行環境

- .net core
- C# 7.0 ~
- vs 2019 <- **must!**

最速の干す手イング環境

- asp.net core + iis
  - linux よりも30%ほど早い

最速のシリアライザ

- messagepack for C#
- Uft8Json

最速のEnum

- Fast Enum
  - じんぐるさん謹製

### **構造体を上手に使う**

GCが動きずらくなる。
構造体はスタック領域(他はヒープ)
GCの発動でパフォーマンス低下につながるのでVRなどに有効

### 構造体の欠点

高頻度で値のコピーが発生
- 関数呼び出しでも発生→defensive copy
  - サイズの大きい構造体の場合、コストになる
- 継承、多態ができない
  - interfaceを使うしかないが、C#8で変わるかも

参照渡しをする！

- 性能劣化に著kk列するコピーの防止
- refばっかりになる
- 構造体が大きい時は　refやoutを検討する

defensive copy(防衛的コピー)の発生
`in`キーワード(読み取り専用)
→refを使おう、もしくは`readonly struct`

C#8以降、関数にreadonlyを付ける

`ValueTuple`

`Span<T>`→ポインタをマネージドに扱える

`String.Create`→ゼロ初期化されたメモリ領域に直で展開

`stackalloc`→

### Avoid Boxing

ボックス化とは、値型を参照型に買い替えること

ボックス化→System.Collectionsはダメ、System.Collections.Genericsに書き換えよう

Enumの罠→System.Enumは参照型

構造体をinterface型として扱うとボックス化

### 非同期I/Oを利用する

CPUは最も高価な計算リソース

並列処理を積極的に使う

```csharp
var t1 = asynca();
var t2 = asyncb();
var t3 = asyncc();

await TaskWhenAll(t1,t2,t3);
```

ValueTask→Taskなどをラップ下構造体

abstract/virtual/interfaceメソッドの戻り値はTaskではなく、ValueTaskにする
非同期でも同期でも対応できる

### 刷らぬ間にできるインスタンスに気を付ける

変数キャプチャ→クロージャなどでは隠しクラスが生成される

LList<T>でadd()しかしないのであれば、LinkedListやArrayでもいいのでは

インライン化

## 始めようAzure Functions

イベントドリブンなアプリケーションを作るためのフレームワーク

Azure App Service

### Azure Functionsの構成要素

トリガーとバインド

トリガーによって関数が実行される
バインドによってトリガーの入力をなににするのか、出力はどこにするのか
などを決定する

トリガー

- http
- strage queue
- blob cosmos db
- event hubs
- timer
- etc...

httpTriggerなど

バインド
関数の入力と戻り値を外部リソースと紐づける

- blob(ファイル置き場)
- queue
- cosmos db
- SignalR Service
- etc...

functions -> SignalR -> devices  
cosmos db -> functions

などの機構が作れる

## クリーンアーキテクチャ

ごめんなさい、マジで内容わかりませんでした

## null許容参照型