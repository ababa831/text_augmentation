# text_augmentation

[Google Translation API](https://cloud.google.com/translate/?hl=ja)を用いて，文書データのAugmentation（サンプル数拡張）を行う．

Google翻訳で，テキストを一度別の言語に翻訳してから元の言語に再翻訳すると，ソーステキストと意味は似ているがテキスト自体は異なる文章が出力されることが多い．
これ応用して，ソース文書と同様の意味を持つが全く新しい文書を生成するコードを作成した．

Kaggleの自然言語処理系コンペでAugmentationが認められている場合は，本コードを応用するとスコアが上がるかもしれない．

## 仕組み

1. 入力された言語を，一時的に別の言語に翻訳する（入力時に指定）
2. 別の言語に翻訳された文書を，元の言語に再翻訳する
3. 再翻訳された文書データを出力する

翻訳，再翻訳はGoogle Translation APIの[Pythonクライアントライブラリ](https://developers.google.com/api-client-library/python/apis/translate/v2)を利用する．


## 使い方

### Requirements
- Python >= 3.4
- Cloud Translation APIとPythonクライアントライブラリが使用できる環境 ([ここのガイドに従う](https://cloud.google.com/translate/docs/quickstart?hl=ja))

### 手順

ソース文書は各自でご用意ください．

1. 本リポジトリを`git clone`する
2. ソース文書(csv形式)をcloneしたディレクトリに追加する
3. cloneしたディレクトリ内にある，`text_augmentation.ipynb`ノートブックを起動する
4. ソース文書をDataFrame形式で読み込む
5. `text_augmentor`メソッドを利用して，Augmentationを試す

### 注意

- **大量の文書データを処理する場合は，予めTranslation APIの[利用料金](https://cloud.google.com/translate/pricing?hl=ja)をシミュレートすることを強く推奨する（下手すると，数百万円課金される可能性あり）**
- Translation APIのquataデフォルト値では，翻訳のリクエスト頻度の上限が処理速度のボトルネックになる
    - 100s当たりで翻訳できるchara(文字)数の上限を引き上げれば，ボトルネックを解消できる ([参考](https://cloud.google.com/translate/limits?hl=ja))
    - サンプル数が多い場合は，一日当たり翻訳できるchara(文字)の上限数も併せて引き上げた方がよい











