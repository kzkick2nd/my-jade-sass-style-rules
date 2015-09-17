実務から得たjade,sass書き方ルール。BEMほどは堅すぎず（構造を示すclassはdiv要素にのみ書くべし）、MCSSのレイヤー構成を利用している前提で以下の様に書く。また変える。

### Jadeの書き方
基本的にちょっと緩いBEM

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
          a(href="").btn button style anchor
  .another-block
    .another-block__item.js_superb-script.is_active
```

### SASSの書き方
&多用しまくる

```sass
%clearfix
  // @extend専用スタイル

.btn
  // 共通のスタイル

.some-block
  // ブロック自体のスタイル

  // ブロックの状態スタイル
  &.is_something

  // 内容物のスタイル
  &__wrap
    // extendは一番上に
    @extend clearfix
    h4
  &__item
    h5
    p
    &__child-item
      a
      a.btn
        // 個別上書き（モヤッとする）

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
- 管理を考えると目に見えている親ブロックから外に汚染しなければそれでよいという気持ちが強い。
- Jadeのクラス名に`&セレクター`使えたらBEM的な書き方は何か解決する気はする。
- 出来上がりのHTML・CSSが冗長ってのが潜在的に気になるが、これはどちらかというとPostCSS的なモノが扱うべき範囲なのでほっておく。GWTで作ったとかいわれるGmailみたいなクラス名処理したい。可読性？生のHTMLとCSSで管理したくない。
- `clearfix`とかよくある共通のモノは`@extend`に追い出す。
- **ベースレイヤー**で用意するもの以外、細かい**OOCSS**はやってはならない。
- .btnなどの扱いにはつくづく悩む。.is_btnにした方がいい？
- BootstrapはBootstrap式書き方にかなり依存するので参考にはすれども使うべき時はすくないという立場
- [カーゴカルトCSS](http://terkel.github.io/cargo-cult-css/)を正座して読んでまた考える。
- というか、もはや似たような文法なんだし、SASSとJADEを合わせた新しいテンプレートエンジンがあればいいんじゃ。

2015 kzkiq2nd
