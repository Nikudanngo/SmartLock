# ESP32 を使用した SmartLock

## 仕組み

1. ESP32 でアクセスポイント(wifi)を立てる
1. と同時にローカルサーバを立ち上げる(web サイト)
1. スマホなどでアクセスポイントに接続してシリアルモニターに表示された IP アドレスにアクセスする
1. /on にアクセスすると LED が点灯し，サーボを 90,180,90 の順に動かす
1. /off にアクセスすると LED が消灯し，サーボを 90,0,90 の順に動かす

## なんで raspberry pi じゃダメなのか？

raspberr pi zero なら今までの仕組みでよかったけど，raspberry pi 4 では電源的に単体のプロダクトにならない問題がありました．つまり，スマートロックにコンセントから電源を持ってくる必要があるということ．
これじゃダサい．．．
また，学校の wifi のセキュリティが高く raspberry pi 通常の wifi 接続ではうまくいかないし，仮にうまくいっても IP アドレスがころころ変わってしまって web ページにアクセスできなくなる可能性もありました．

## ESP32 すげー

そこで ESP32 を使ってみました．これは上記の問題をすべて解決してくれます．
ESP32 は 3V1A で動作し 5V の出力に対応します．つまり，モバイルバッテリーで動作しこれ単体でサーボも動く．さらに，wifi モジュール周りのライブラリが充実してて簡単にアクセスポイントを立てられるので ESP32 が wifi に接続しなくても電源を入れるだけでローカルサーバを立てられるようになりました．
