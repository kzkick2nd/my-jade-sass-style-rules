個人用のjade,sass書き方ルール。BEMほどは堅すぎず、SMACCSくらいにはゆるく、MCSSのレイヤー構成を利用している前提で以下の様に書く。また変える。

### Jadeの書き方
基本的に緩いBEM

```jade
body.page__some-page.prefix
  .some-block.is_something
    .some-block__wrap
      h4 Some title
      .some-block__item
        h5 Some subtitle
        p Some paragraph
        .some-block__item__child-item
          a(href="") Some anchor
  .another-block
    .another-block__item.js_superb-script.is_active
```

### SASSの書き方
&多用しまくるのはセレクター数上限に気をつけないとあかん。

```sass
.some-block
  // ブロック自体のスタイル

  // ブロックの状態スタイル
  &.is_something

  // 内容物のスタイル
  &__wrap
    h4
  &__item
    h5
    p
    &__child-item
      a

  // ページ個別のスタイル
  .page__some-page &

  // その他のprefix(ブラウザとか、loginとか)
  .prefix &

// jsによる状態変化
.another-block
  &__item
    &.js_superb-script
      &.is_active
```

### 考えていること
- 管理を考えると今目に見えているブロックから外に汚染しなければそれでよいという気持ちが強い。
- Jadeのクラス名に`&セレクター`使えたら何か解決する気はする。
- 出来上がりのHTML・CSSが冗長ってのが潜在的に気になるが、これはどちらかというとPostCSS的なモノが扱うべき範囲なのでほっておく。GWTで作ったとかいわれるGmailみたいなクラス名処理したい。可読性？生のHTMLとCSSで管理したくない。
- `clearfix`とかよくある共通のモノは`@extend`に追い出す。
- **ベースレイヤー**で利用されているもの以外、細かい**OOCSS**はやらない。


2015 kzkiq2nd
