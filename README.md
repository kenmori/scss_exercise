# SCSS問題集

こちらはSCSSです。
問題を解いて苦手意識があったディレクテブをやや使えるようになるのを目指すページです。
※答えはあくまで一例ですのでもっと端的に書ける、別の方法のほうがいいというのであればそれが答えです。
ここでいう答えはエラーを出さず問題を解消、実現できる1つの方法です

問1

@ifを用いて$aが"eee"ならpのfont-colorをblue、それ以外をred

```scss
$a : "eee";
p {
  @if $a == "ee" {
    font-color: "blue"
  } @else {
    font-color: "red"
  }
}
```

問2
@eachを用いてp.aにa.png、p.bにb.png、同様にc、dに背景画像を適応するコード

```scss
$arry : a,b,c,d;
@each $arr in $arry {
 p.#{$arr}{
   background: url("/resources/fafa/#{$arr}.png");
  }
}
```

問3
@eachを用いてkey,valueを扱う

```scss
$colors:(
  'page': red,
  'pageA': green,
  'pageB': blue
);
@each $key, $value in $colors {
  p.#{$key} {
    background: url(/resources/img/#{$value}.png);
  }
}

```

問4
list内のcが何番目かを出力

```scss

$list: a, b, c;
p {
  .fafa : index($list, c);//index: number (list, list.item);
}
//listは
$list: a b c;
でも問題ない

```

問5
liの数だけindexに対して独自の画像を当てる

```scss

$kv: 'twitter','facebook';
@each $k in $kv {
  $i: index($kv, $k);//List型しかできない
  li:nth-child(#{$i}){
    background: url(/resouces/img/#{$k}.png);
  }
}

```

問6
1~nまで繰り返し(今回は1から10まで)、そのインデックスをとってプロパティやクラス名として使う

```scss
$number: 10;
@while $number > 0 {
  .class-#{$number} {
    background: url(img/#{$number});
  }
  $number: $number - 1;
}


$num : 5;
@while $num > 0 {
  .u-fs#{$num * 10} {
    width: 10 * $num + 'px';
  }
  $num: $num - 1;
}



//other
@for $i from 1 to 10 {
  .class-#{$i} {
    width: #{$i}px;
  }
}
```


問7
SASSとSCSSの違いとは

```scss
//記法の違い
・ブラケット有無
・セミコロン有無
・インデント有無

//.sass
div
    margin: 0 auto
    p
        padding: 20px
        span
            font-color: red;

//.scss
div {
    margin: 0 auto;
    p {
        padding: 20px;
        span {
             font-color: red;
        }
    }
}
```

問8

```scss
@function halfWidth($width: 50px){
  @return $width / 2;
}
p {
  width: halfWidth(100px);
}
```

問9

色を投げると.5のopacityになるrgba組み込み関数

```scss
.classe {
  color: rgba(#fff, 0.5);
}
```


問10

mixinが存在していれば#fffをなければ#000を指定する

```scss
@mixin arrow {
  color: #e2e2e2;
}
.mixin-exits {
  &:before {
    color: if(mixin-exists(arrow), #fff, #000);
  }
}
```


問11

```scss
//unitless 指定した数値が単位を持っていればfalse,　持ってなければtrue

@mixin caluclate($x, $y){
  @if unitless($x){
    @warn "渡す際pxをつけることを忘れています : #{$x}";
    $x: 1px * $x;
  }
  @if unitless($y){
    @warn "渡す際pxをつけることを忘れています : #{$y}";
    $y: 1px * $y;
  }
  position: relative;
  left: $x;
  top: $y;
}

.ul {
  @include caluclate(7, 2);
}
```

問12

単位を持っていたらture、持っていなかったらfalseを返す
```scss
.ul {
  content: if(unit(100px), 100, 200);//"px"
}
```

問13

funcという独自関数が存在するか、valueという変数が存在するか、グローバルスコープにgvalue変数が存在するかを調べてください


```scss


//1
//もしfunc関数が定義されていたら実行、ないなら5
function-exists(func)//false
li {
  color: if(function-exists(func), func(), 5);
}
//5

//2
//もし$valueが定義されていたらその値を、ないなら#fffを
$value: #ccc;
li {
  color: if(valuable-exists(value), $value, #fff);
}
```

問14
colorオブジェクトでkey-valueで値を管理、.color内のcolorの値として取得する

```scss

$colors: (
  brand-red: #c0392b,
  brand-blue: #2980b9,
  text-gray: #2c3e50,
  text-sliver: #bdc3c7
);
.color {
  color: map-get($colors, brand-red);
}
```

問

```scss
$colors: (
  brand-red: #c0392b,
  brand-blue: #2980b9,
  text-gray: #2c3e50,
  text-sliver: #bdc3c7,
);
$borderColors: (
  red: red,
  green: green
);
```

こちらをmergeして
contentプロパティの値としてkey名を出力してください

```scss
$colors: (
  brand-red: #c0392b,
  brand-blue: #2980b9,
  text-gray: #2c3e50,
  text-sliver: #bdc3c7,
);
$borderColors: (
  red: red,
  green: green
);

$newColor: map-merge($colors, $borderColors);

li {
  content: map-keys($newColor);
  color: map-get($newColor, red);//$newColorの中から選ぶ
}
```

問
breakpointのmixinを作りたい。
smallを767px, mediumを992px, largeを1200pxとしたブレイクポイントをそれぞれのkeyを渡すと作ってくれるmixinを作成、もしsmallが渡って来たらcolor:#fffとするように任意のセレクタに対して読み込んでください

```scss

$breakpoints: (
  small: 767px,
  medium: 992px,
  large: 1200px
);

@mixin widthCreator($breakpoint){
  @if map-has-key($breakpoints, $breakpoint) {
    @media (min-width: #{map-get($breakpoints, $breakpoint)}){
     @content;
    }
  } @else {
    @warn "not exists key"
  }
}
li {
  color: 000;
  @include widthCreator(small){
    color: #fff;
  }
}
```

問
下記

```scss
.fa-glass:before {
  content: "\f000";
}
.fa-music:before {
  content: "\f001";
}
.fa-search:before {
  content: "\f002";
}
.fa-envelope-o:before {
  content: "\f003";
}
.fa-heart:before {
  content: "\f004";
}
```
を@eachで生成してください

```scss
$icons: (
  glass: "\f000",
  music: "\f001",
  search: "\f002",
  envelop-o: "\f003",
  heart: "\f004"
);
@each $key, $value in $icons {
  li.fa-#{$key}:before {
    content: $value;
  }
}

```

問
下記のこちら

```scss
@mixin SelectorCreator ($value: 30px){
  width: 100px;
  padding: $value;
}

.class {
  @include SelectorCreator(10px);
}
.class2 {
  @include SelectorCreator(20px);
}
```
を$valueを渡さなくても(引数なしでも)padding値が呼び出し元で渡せる記述をしてください

```scss
@mixin SelectorCreator (){
  width: 100px;
  @content;
}

.class {
  @include SelectorCreator(){
    padding: 10px;
  }
}
.class2 {
  @include SelectorCreator(){
    padding: 20px;
  }
}
```

問

mixinとextendsのユースケースは

```scss
mixin ・・・重複する箇所に値を動的に挿入する時か、Single Source of Truthを保ちながらプロジェクト全体を通して同じ宣言のグループを繰り返すことのできるSassyのコピー＆ペーストとして使う時にしましょう。(引数を渡せる)

extend・・・ @extend は、DRYにしようとするルールセットが本質的、テーマ的に関係性がある時だけ使いましょう。存在しない関連性を無理に作ってはいけません。もし、それをやってしまうと、プロジェクトの中で異常なグルーピングが行われてしまい、コードのソースの順序に悪影響を及ぼしてしまいます

see: http://postd.cc/when-to-use-extend-when-to-use-a-mixin/
```


参照
http://postd.cc/when-to-use-extend-when-to-use-a-mixin/

