Hugo の {{define}}-{{template}} を理解する
==========================================

* `{{define}}` は layouts 配下のどのファイルに書かれていても最初に全て適用（定義）される
    * このため例えば _index.html_ と _\_default/single.html_ で同名の `{{define}}` を書くと  
    __template: redefinition of template "hoge"__  
    と言われてエラーになる
* どこからも参照されない layouts 配下のファイル（拡張子が何でも）に `{{define}}` を書いておくこともできる
* `{{define}}` 内の名前空間は `{{template}}` のふたつめのパラメタ（pipeline）になるので定義されるファイルの名前空間とは無関係
    * _SECTION1/single.html_：`{{define "fuga"}}{{.Section}}{{end}}`
    * _SECTION2/single.html_：`{{template "fuga" .}}` → SECTION2
* つまり `{{define}}` はファイルを分離しない partial のようなもので、変数のような使い方はできない
    * Djangoの `{% block %}`-`{% extends %}` とは考え方が違う
