# Jestの基本
[Jest](https://jestjs.io/ja/)はFacebook社によって作られたJS/TSのテストフレームワーク。単体テスト、結合テストを効率よく書くことができる



```
npm install -D jest
or
yarn install -D jest
```

## 基本的なマッチャー
**基本的な`expect`関数に関連するマッチャーの種類**

`expect()`は`expectation`オブジェクトを返す。それだけでは意味はなくマッチャーをつくことで意味をなす。


### ・`toBe(value)`

期待値を`===`での比較と同じように比較する。（厳密に型をみる）

```js
test("テスト名", () => {
    expect(1 + 1).toBe(4);
});
```


### ・`toEqual(value)`

**オブジェクト**や**配列**のすべてのプロパティ、値が等しいかをチェックする。<br />
`toBe`でオブジェクトや配列の審査をする場合は、同じ値でも参照が違うと`false`になる。<br />
`toEqual`の場合、**値が同じなら、参照が違っても`true`となる。**

```js
test("テスト名", () => {
    const obj = {one: 1, two: 2}
    const array = [1, 2, 3]

    expect(obj).toEqual({one: 1, two: 2});
    expect(obj).toEqual([1, 2, 3]);
})
```
1. **型の変換を許容する**
```js
test("テスト名", () => {
    const obj = {one: "1", two: 2}//文字列の1

    expect(obj).toEqual({one: 1, two: 2});//成功する
})
```
2. **未定義（undefined）と欠落しているプロパティを区別しない**
```js
test("テスト名", () => {
    expect({a: undefined}).toEqual({});//成功する
})
```

### ・`toStrictEqual(value)`

`toEqual`よりオブジェクトや配列を厳密に検査して一致しているかを確認する。
1. **型の変換を許容しない**
```js
test("テスト名", () => {
    const obj = {one: "1", two: 2}//文字列の1

    expect(obj).toStrictEqual({one: 1, two: 2});//失敗する
})
```
2. **未定義（undefined）と欠落しているプロパティを区別する。**
```js
test("テスト名", () => {
    expect({a: undefined}).toStrictEqual({});//失敗する
})
```

## 修飾子

### ・`not.`
マッチャー逆のアサーションを行う
```js
test("テスト名", () => {
    expect({a: undefined}).not.toStrictEqual({});//成功する
})
```

### ・`resoles.`

### ・`rejects.`


## 論理値のマッチャー

### ・`toBeNull(value)`
値が`null`であることを確認する。
```js
test("テスト名", () => {
    expect(null).toBeNull();
})
```

### ・`toBeUndefined(value)`
値が`未定義（undefined）`であることを確認する。
```js
test("テスト名", () => {
    expect(undefined).toBeUndefined();
})
```

### ・`toBeDefined(value)`
値が`undefined`でないことを確認する。
```js
test("テスト名", () => {
    expect("定義").toBeDefined();
})
```

### ・`toBeTruthy(value)`
値が`true`であることを確認する。
```js
test("テスト名", () => {
    expect(true).toBeTruthy();
})
```

### ・`toBeFalsy(value)`
値が`false`であつことを確認する。
```js
test("テスト名", () => {
    expect(false).toBeFalsy();
})
```

## 数値のマッチャー

### ・`toBeGreaterThan(number)`
値が期待値**よりも大きい**ことを確認する。
```js
test("テスト名", () => {
    expect(4).toBeGreaterThan(3);//成功
    expect(4).toBeGreaterThan(4);//より大きくないので失敗
})
```
### ・`toBeGreaterThanOrEqual(number)`
値が期待値**以上**であることを確認する。
```js
test("テスト名", () => {
    expect(4).toBeGreaterThanOrEqual(4);//以上なので成功
})
```

### ・`toBeLessThan(number)`
値が期待値**よりも小さい**ことを確認する。
```js
test("テスト名", () => {
    expect(4).toBeLessThan(5);//成功
    expect(4).toBeLessThan(4);//失敗
})
```

### ・`toBeLessThanOrEqual(number)`
値が期待値**以下**であることを確認する。
```js
test("テスト名", () => {
    expect(4).toBeLessThanOrEqual(4);//成功
})
```

### ・`toBe(number), toEqual(number)`
`toBe`と`toEqual`は数値において同じ動きである。
```js
test("テスト名", () => {
    expect(4).toBe(4);//成功
    expect(4).toEqual(4);//成功
})
```

### ・`toBeCloseTo(number, digits?)`
浮動小数点の数値については丸め誤差を防ぐ観点から`toBeCloseTo`を使用する。
```js
test("テスト名", () => {
    expect(0.123456789).toBeCloseTo(0.12345678, 8);//成功
    expect(0.123456789).toBeCloseTo(0.12345678, 9);//失敗
})
```

## 文字列のマッチャー
### ・`toMatch(reg | str)`

### ・`toContain(str)`


## 配列とiterableなオブジェクトのマッチャー

### ・`toContain(item)`
### ・`toHaveLength(number)`

## オブジェクトのマッチャー

## 例外（Exception）のマッチャー

## 補足
### TDDについて
テスト駆動開発のゴール→「動作する綺麗なコード」

「動作する」と「綺麗なコード」を分ける

### TDDのサイクル
1. 目標を考える
2. 目標を示すテストを書く
3. そのテストを実行して失敗させる（RED）
4. 目的のコードを書く
5. 2で書いたコードを成功させる（Green）
6. テストが通るままリファクタリングをする
7. 1~6を繰り返す


### オススメの参考書
ソフトウェアテスト技法練習帳
ソフトウェアテスト技法ドリル