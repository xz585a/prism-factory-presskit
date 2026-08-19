# Prism Factory — Press Kit

『Prism Factory』のプレスキット。GitHub Pages で公開する。

**公開 URL: https://xz585a.github.io/prism-factory-presskit/**
**Steam: https://store.steampowered.com/app/5114180/**

この URL は3回のプレスリリースすべてで使い回す。**変えない。**

前作（`033-desktop-smith` / [desktop-forge-presskit](https://github.com/xz585a/desktop-forge-presskit)）
と同じ構成で、運用の考え方もそのまま引き継いでいる。

## 言語切り替え

ページ右上のボタンで日本語と英語を切り替える。**本文だけでなく、素材のキャプションや
ボタンのラベルも含めて全体が切り替わる。**

- 初期表示はブラウザの言語設定で決まる（日本語環境なら日本語、それ以外は英語）
- 選んだ言語は `localStorage` に保存され、次回以降そちらで開く
- JS が無効な場合は両言語とも表示される（情報が消えないことを優先）

**テキストを追加するときは、必ず日英の両方を書く。** 片方だけ書くと、その言語では
何も表示されない。マークアップは `class="l-ja"` / `class="l-en"` の対で置く。

```html
<figcaption><span class="l-ja">マップ選択</span><span class="l-en">Map select</span></figcaption>
```

**切り替わるのは文章だけで、素材は日英で同じものを出す。** 本作は画面に文字がほとんど出ないため、
スクリーンショットもループ動画もトレーラーも、言語別に用意しない
（前作は日本語UI・英語UIの2組を持っていた。ここは意図的に違う）。
**したがって素材のファイル名に言語の接尾辞は付けない。**

## 中身

```text
.
├── index.html          プレスキット本体（日英を1ページに併記）
├── fact_sheet_ja.txt   日本語のファクトシート（配布用テキスト）
├── fact_sheet_en.txt   英語のファクトシート
├── build_thumbs.py     原寸から一覧表示用の縮小版を作る
├── assets/
│   ├── images/         スクリーンショット（原寸 PNG）
│   ├── thumbs/         一覧表示用の縮小版 WebP  ※自動生成。直接編集しない
│   ├── branding/       ロゴ・カプセル画像（Steam へ出したものと同じ原寸）
│   ├── gifs/           ループ動画（mp4、無音）
│   └── video/          トレーラーの mp4  ※Git 管理外
└── downloads/          一括ダウンロード用の zip  ※Git 管理外
```

場面の番号と名前は、ゲーム本体側の `marketing/施策/撮影リスト.md` の考え方に合わせている。

**ファイル名は公開URLとして固定しているので変えない。**ゲーム本体側の素材フォルダから
持ち込むときにリネームする。命名は `<番号>_<名前>.png`。

**題名の表記に注意する。**文字として出るところは全て `Prism Factory`。
`PRISM FACTORY` と全大文字にしない ── 大文字なのは描かれたロゴだけで、
それはマークであって語ではない（ゲーム本体側の `docs/00_concept.md` §9）。
**プレスキットの本文は編集部がそのまま記事へ写すので、ここでの表記がそのまま外に出る。**

## 現在の収録物

- スクリーンショット **12枚**（無加工の PNG。11枚は 1920×1080、`02_board_wide` のみ 3840×2160）
- ループ動画 **7点**（mp4、無音、1〜7秒）
- ロゴ（透過 PNG）を含むブランド素材10点（`assets/branding/`。Steam へ出したものと同じ原寸）
- ファクトシート 日英
- トレーラー（82秒、20MB に再圧縮した mp4）

**素材は全て日英で共用する。**本作は画面に文字がほとんど出ないので、
スクリーンショットもループ動画もトレーラーも、言語別に撮り分けない。

### 未収録（撮れ次第、足す）

| 何 | 備考 |
| --- | --- |
| セッション終了時の記録の画 | 撮影リスト A-09 |
| タイトル画面 | 撮影リスト A-08 |
| トレーラーの YouTube 版 | 下記「トレーラー」 |

## 配布アセットの置き場

**zip とトレーラーの mp4 は、リポジトリに入れない。** GitHub Releases の `assets`
タグへ置き、ページからはそこへリンクする。

```text
https://github.com/xz585a/prism-factory-presskit/releases/download/assets/PrismFactory_PressKit.zip
https://github.com/xz585a/prism-factory-presskit/releases/download/assets/PrismFactory_Trailer.mp4
```

理由は、**この2つだけが繰り返し差し替わるうえに大きい**こと。Git はバイナリの差分を
持てないので、作り直すたびに丸ごと履歴へ積み上がり、あとから減らせない。

更新は**同じファイル名で上書き**する。URL が変わらない。

```bash
gh release upload assets downloads/PrismFactory_PressKit.zip --clobber
```

**公開前に、この2つを Releases へ上げておくこと。**ページ上のトレーラーと
一括ダウンロードのリンク先がこの URL なので、上げるまでは 404 になる。

**手元で開いたときだけは、トレーラーが `assets/video/` から再生される。**
`index.html` の末尾に、`localhost` と `file://` でだけ `src` を差し替える数行を入れてある。
Releases がまだ空の状態でも、ページの見え方を確認できる。
**GitHub Pages 上では効かない**（`assets/video/` は Git 管理外なので存在しない）。

```bash
gh release create assets --title assets --notes "press kit assets" || true
gh release upload assets assets/video/PrismFactory_Trailer.mp4 --clobber
gh release upload assets downloads/PrismFactory_PressKit.zip --clobber
```

スクリーンショットの PNG とループ動画は、これまでどおり Git で管理する。
配布物そのもので、差し替えの頻度も低いため。**ただしコミットするのは公開する確定版だけ**にする
（撮り直しの途中経過を入れると、上と同じことが起きる）。

### 画像形式と、原寸／縮小版の分担

配布する原寸は **PNG。**盤面は細い線と発光でできており、JPEG の圧縮では光の縁に滲みが出る。
編集部は記事用に一部を切り出して拡大するので、そこで粗が見える。
ShareX は「ファイルサイズが一定を超えたら別形式で保存する」設定があるため、
**その閾値を外して常に PNG で保存する。**

原寸を一覧に並べるとページが重くなり、回線の細い環境では開かれずに閉じられる。
そこで**表示と配布を分けている。**

| 置き場 | 形式 | 役割 |
| --- | --- | --- |
| `assets/images/` | PNG（原寸） | クリック時のリンク先。zip の中身。**これが配布物** |
| `assets/thumbs/` | WebP（幅960px） | 一覧表示のみ。1枚 12〜71KB |

縮小版は手で作らない。**スクリーンショットを差し替えたら `build_thumbs.py` を実行する。**

```bash
python build_thumbs.py
```

原寸が消えた分の縮小版は自動で削除される。`assets/thumbs/` を直接編集しない。

## トレーラー

いまはページに `<video>` を置き、Releases の mp4 を直接再生している。
元素材（ゲーム本体側の `marketing/trailer/完成/prism_factory_trailer_01.mp4`、83MB）を
ffmpeg で 20MB へ再圧縮したものである。

```bash
ffmpeg -i prism_factory_trailer_01.mp4 -c:v libx264 -preset slow -crf 22 \
  -pix_fmt yuv420p -movflags +faststart -c:a aac -b:a 128k \
  assets/video/PrismFactory_Trailer.mp4
```

**YouTube へ上げたら、`#trailer` セクションの `<video>` を
`youtube-nocookie.com/embed/<id>` の iframe へ差し替える**（`class="trailer-player"` は
そのまま使う）。mp4 のダウンロードリンクは残す ── 編集部が使う。

**iframe にもインライン `style` で `display` を書かないこと。** 言語切り替えの
`display:none` に勝ってしまう。高さは `.trailer-player` の `aspect-ratio: 16 / 9` が
担っている（iframe には固有の縦横比がないため、これを外すと潰れる）。

なお**このトレーラーには字幕が無く、日英で1本を共有している。**
字幕版を分けて作ることになったら、`<video>` を `l-ja` / `l-en` の対にする。

## zip の作り直し

素材を追加・差し替えたら zip も作り直し、**Releases へ上書きアップロードする**。
zip 自体はコミットされない。

```bash
python - <<'EOF'
import os
import zipfile

out = "downloads/PrismFactory_PressKit.zip"
os.path.exists(out) and os.remove(out)
z = zipfile.ZipFile(out, "w", zipfile.ZIP_DEFLATED)
for f in ["fact_sheet_ja.txt", "fact_sheet_en.txt"]:
    z.write(f, "PrismFactory_PressKit/" + f)
for sub in ["assets/images", "assets/gifs", "assets/branding"]:
    for f in sorted(os.listdir(sub)):
        if not f.startswith("."):
            z.write(os.path.join(sub, f), "PrismFactory_PressKit/" + sub.split("/")[1] + "/" + f)
z.close()
EOF
gh release upload assets downloads/PrismFactory_PressKit.zip --clobber
```

## 素材を追加したときの手順

1. ファイルを `assets/images/`（原寸）へ置く。命名は `<番号>_<名前>.png`
2. `python build_thumbs.py` を実行して縮小版を作り直す
3. `index.html` の対応する `<figure>` を足す（`figcaption` は日英の対で書く）
4. zip を作り直し、Releases へ上書きアップロードする
5. コミットして push する。GitHub Pages への反映は数十秒〜数分

## 公開の手順（初回）

```bash
gh repo create prism-factory-presskit --public --source . --remote origin --push
```

push したら、リポジトリの Settings → Pages で **Source を `Deploy from a branch`、
Branch を `main` / `(root)`** にする。数十秒で
`https://xz585a.github.io/prism-factory-presskit/` が開く。

その後、上の「配布アセットの置き場」のコマンドで zip とトレーラーを Releases へ上げる。

## 制約

- **1ファイル 100MB まで**（Releases 側は 2GB まで）。ページに直接置く mp4 は
  20〜30MB に収め、原寸は Releases か YouTube へ逃がす
- サイト全体で 1GB まで
- **このリポジトリはパブリック。** 未公開の情報を含むファイルを置かない
