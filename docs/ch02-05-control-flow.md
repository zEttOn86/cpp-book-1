# 制御文

## if

条件分岐をしたい時には `if` を使用します。

```cpp
int x = 5;

if (x == 5) {
    ...
}
```

`if` の条件を満たさなかった場合に何か処理をしたければ `else` を使用します。

```cpp
int x = 5;

if (x == 5) {
    ...
} else {
    ...
}
```

さらに別の条件で処理を分岐したければ `else if` を使用します。

```cpp
int x = 5;

if (x == 5) {
    ...
} else if (x == 6) {
    ...
} else {
    ...
}
```

## switch

一つの変数の値を調べながら分岐するような処理を書きたい場合は `switch` 文を使います。

```cpp
switch (x) {
    case 0:
        // x == 0 のときの処理
        break;
    case 1:
        // x == 1 のときの処理
        break;
    default:
        // x がそれ以外のときの処理
        break;
}
```

ただし `switch` 文が使用できるのは基本型のみです。
上記の構文は `if` で書き直すと次と等価になります。

```cpp
if (x == 0) {
    // x == 0 のときの処理
} else if (x == 1) {
    // x == 1 のときの処理
} else {
    // x がそれ以外のときの処理
}
```

ただし `switch` 文のほうが `if` よりも比較回数が少ないため効率的です。
`if` はまずはじめに `x == 0` が `true` かどうかを調べ `false` であれば
次に `x == 1` を評価しますが、`switch` 文はいきなり特定の `case` にジャンプします。

### フォールスルー

`switch` の各 `case` 内に書かれている `break` は書かなくてもよいのですが、
その場合振る舞いが変わります。

```cpp
switch (x) {
    case 0:
        // x == 0 のときの処理
    case 1:
        // x == 1 のときの処理
    default:
        // x がそれ以外のときの処理
}
```

`break` を書いた場合は `switch` 文の処理はそこで終わりますが、
`break` を書かなかった場合はそのまま下の `case` に処理が流れてしまいます。
つまり上記のコードは `x == 0` であれば `case 0` 内の処理を行った後に
`case 1` 内の処理を行い、最後に `default` の処理を行います。
`x == 1` であれば同様の振る舞いが `case 1` から始まります。
このような `switch` 文の仕様をフォールスルーと言います。
これは `case 0` と `case 1` の処理が同じものになる場合に使用すると便利です。

```cpp
switch (x) {
    case 0:
    case 1:
        // x == 0 または x == 1 のときの処理
    default:
        // x がそれ以外のときの処理
}
```

それ以外のケースでフォールスルーをさせるシーンはまずないため、
`break` を忘れずに付けておく必要があります。

## while

`while` は `()` に渡された条件が `true` である限り
`{ ... }` 内の処理を実行し続けます。

```cpp
int x = 5;
bool done = false;

while (!done) {
    x += x - 3;

    std::cout << x << std::endl;

    if (x % 5 == 0) {
        done = true;
    }
}
```

## for

`for` はループするたびに変化する変数を使うことができます。

```cpp
for (int i = 0; i < 10; ++i) {
    std::cout << i << std::endl;
}
```

`i` はループするたびに `0, 1, 2, ..., 9` と値が変化し続けます。
`for (int i = 0; i < 10; ++i)` というのは `i` に `0` を設定して
`i < 10` を満たすまで `i` を `+1` しながらループを継続するという意味になります。

### 配列のループ

配列のループは `for` を使って次のように書くことができます。

```cpp
int x[] = {0, 1, 2, 3, 4};

for (auto e : x) {
    std::cout << e << std::endl;
}
```

`e` には 0 から 4 が順に代入されていきます。
`std::array` でも同じように書くことができます。
`for` の中で添字が必要な場合は添字をループして配列の要素をたどります。

```cpp
int x[] = {0, 1, 2, 3, 4};

for (int i = 0; i < 5; ++i) {
    std::cout << x[i] << std::endl;
}
```