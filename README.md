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


