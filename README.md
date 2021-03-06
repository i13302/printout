# printout

## Abstruct
markdownからPDF( `markdown+css→HTML→PDF` )を出力する取り組み．   
大量のドキュメントを前提とし，GitHub Actionsで，1ドキュメント1PDFに変換する．  
現状の生成物は，各Actionsの実行結果を確認のこと．    

## markdown+css→HTML
CSSなどのスタイルやレイアウトは，授業資料とか技術系のドキュメントなど，自由に組み込める．  
CSSや画像はbase64 encodeし，単一HTMLとして出力する．  
pandocをbaseとした `i13302/pandoc`イメージを用いる．  

## HTML→PDF
Chromeの [Page.printToPDF](https://chromedevtools.github.io/devtools-protocol/tot/Page/#method-printToPDF) 機能を用いる．  
A4サイズでのPDF化，日付のヘッダーやページ番号のフッターの付与が実現する．  
`i13302/printout`イメージを用いる．

## Status
- [x] MarkdownからCSSを維持したHTMLファイルの生成
- [x] HTMLファイルからPDFの生成
- [x] ヘッダーやフッターを持つPDFの生成
- [x] 一連の実行を1手順での自動化
- [x] 大量のドキュメントへの対応

## Usage
### Project Download
```
git clone https://github.com/i13302/printout.git
cd printout
```

### Get Image
#### Docker Pull
[Package pandoc](https://github.com/i13302/printout/pkgs/container/pandoc)
[Package printout](https://github.com/i13302/printout/pkgs/container/printout)

```:shell
docker pull ghcr.io/i13302/pandoc
docker pull ghcr.io/i13302/printout
```

#### Local Build
```:shell
make build
```

Builded Image `i13302/pandoc` and `i13302/printout`. 

### Build Text
Create dir is used this system.
```:shell
make setup
```

Result.
```
$ tree work/
work/
├── base
├── css
├── html
├── markdown
└── pdf
```

The markdown text into `work/markdown` dir and css into `work/css` dir.    

```:shell
make run
```

### Product PDF
markdown is builded to PDF file in `work/pdf` dir.

### Clean up builded files
remove `work/html/*` and `work/pdf/*`.

```:shell
make clean
```

### Test
This is builded in `test` dir.

#### Build Text
```Sample:shell
make test_run
```

### Clean up
```Sample:shell
make test_clean
```

## License
[MIT License](./LICENSE).
