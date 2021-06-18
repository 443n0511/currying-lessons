# 辛いコードを甘くするカリー化のレシピ
こちらはカリー化についての勉強会資料です。

動作確認用のコードになります。
詳しい解説はブログに記載しています[私のブログ記事](https://monatamalog.com/archives/403)

### 配列からデザートメニューだけを取り出す

こちらの配列の中からデザートだけを取り出していきます
```js
const menus = [
    { menu: 'ハンバーガー', type: 'burger' },
    { menu: 'チーズバーガー', type: 'burger' },
    { menu: 'ソフトクリーム', type: 'dessert' },
    { menu: 'ポテト', type: 'side' },
    { menu: 'チキンナゲット', type: 'side' },
    { menu: 'ホットアップルパイ', type: 'dessert' },
    { menu: 'コーラ', type: 'drink' },
    { menu: 'オレンジジュース', type: 'drink' }
];
```

#### for文の場合
```js
const dessertMenus = [];
for (let i = 0; i < menus.length; i++) {
    if (menus[i].type === 'dessert') {
        dessertMenus.push(menus[i]);
    }
}
console.log(dessertMenus);
//[ { menu: 'ソフトクリーム', type: 'dessert' }, { menu: 'ホットアップルパイ', type: 'dessert' } ] 
```

#### 高階関数を使った場合
```js
const isDessertMenus = menu => {
    return menu.type === 'dessert';
};
const dessertMenus = menus.filter(isDessertMenus);
console.log(dessertMenus)
//[ { menu: 'ソフトクリーム', type: 'dessert' }, { menu: 'ホットアップルパイ', type: 'dessert' } ] 
```

#### カリー化・部分適用を用いた場合

##### 通常関数で書いた場合
```js
function menuType(type) {
    return function (menu) {
        return menu.type === type
    };
}
const dessertMenus = menus.filter(menuType("dessert"));
console.log(dessertMenus)
//[ { menu: 'ソフトクリーム', type: 'dessert' }, { menu: 'ホットアップルパイ', type: 'dessert' } ] 
```

##### アロー関数で書いた場合

```js
const menuType = type => menu => menu.type === type;
const burger = menus.filter(menuType('burger'));
const dessert = menus.filter(menuType('dessert'));
console.log(dessertMenus)
//[ { menu: 'ソフトクリーム', type: 'dessert' }, { menu: 'ホットアップルパイ', type: 'dessert' } ] 
```
