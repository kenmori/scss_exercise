# scss_exercise



@ifを用いて$aが"eee"ならfont-colorをblue、それ以外をred

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

//@eachを用いてp.aにa.png、p.bにb.png、同様にc、dに背景画像を適応するコード

```scss
$arry : a,b,c,d;
@each $arr in $arry {
 p.#{$arr}{
   background: url("/resources/fafa/#{$arr}.png");
  }
}
```

//@eachを用いてkey,valueを扱う

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
//////////////////
//list内のcが何番目かを出力

```scss

$list : a, b, c;
p {
  .fafa : index($list, c);//index: number (list, list.item);
}

////////
liの数だけindexに対して独自の画像を当てる

$kv: 'twitter','facebook';
@each $k in $kv {
  $i: index($kv, $k);//List型しかできない
  li:nth-child(#{$i}){
    background: url(/resouces/img/#{$k}.png);
  }
}

```

////
1~nまで繰り返し(今回は1から10まで)、そのインデックスをとってプロパティや値として使う

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

```
