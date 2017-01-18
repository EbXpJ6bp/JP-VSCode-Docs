# November 2016 (version 1.8)

## 1.8.1 Recovery Build

年末までにいくつかの[重要な問題](https://github.com/Microsoft/vscode/issues?q=is%3Aissue+milestone%3A%22November+Recovery+2016%22+is%3Aclosed)へ取り組むために、1.8.1 リカバリビルドをリリースしました。 早期に問題発見いただきありがとうございました。

* Fixed scrolling in large minified files ([#17208](https://github.com/Microsoft/vscode/issues/17208))
* Resolved an issue with Copy command in certain contexts ([#17232](https://github.com/Microsoft/vscode/issues/17232))
* Fixed an issue with saving files on a mounted drive ([#17345](https://github.com/Microsoft/vscode/issues/17345))
* Fixed Quick Outline in Default Keyboard Shortcuts ([#17376](https://github.com/Microsoft/vscode/issues/17376))
* Removed 'Focus 既定の設定' command from Command Palette ([#17468](https://github.com/Microsoft/vscode/issues/17468))

VS Code は自動的に 1.8.1 にアップデートしますが、以下のリンクから直接リリースをダウンロードすることも可能です:

Downloads: [Windows](https://vscode-update.azurewebsites.net/1.8.1/win32/stable) | [Mac](https://vscode-update.azurewebsites.net/1.8.1/darwin/stable) | Linux 64-bit: [.tar.gz](https://vscode-update.azurewebsites.net/1.8.1/linux-x64/stable) [.deb](https://vscode-update.azurewebsites.net/1.8.1/linux-deb-x64/stable) [.rpm](https://vscode-update.azurewebsites.net/1.8.1/linux-rpm-x64/stable) | Linux 32-bit: [.tar.gz](https://vscode-update.azurewebsites.net/1.8.1/linux-ia32/stable) [.deb](https://vscode-update.azurewebsites.net/1.8.1/linux-deb-ia32/stable) [.rpm](https://vscode-update.azurewebsites.net/1.8.1/linux-rpm-ia32/stable)

## 11 月リリース版の概要 (November Release Summary)

Visual Studio Code 11 月リリース版へようこそ。 このリリースではいくつかの重要な更新があり、ハイライトは次のとおりです:

* **[Hot Exit](#hot-exit)** - 未保存のファイル変更を失いません
* **[Focus on Your Code](#focus-on-your-code)** - 禅モード、設定可能なアクティビティバーなどの機能強化
* **[Settings improvements](#settings)** - VS Code を設定するための新しい設定画面
* **[New Selection menu](#selection-menu)** - エディタ上での選択コマンドをメニューに配置
* **[Faster Text Search ](#text-search-performance)** - プロジェクトの規模に関係なく、より高速にコードを検索
* **[Snippet authoring](#snippets)** - コードスニペットで変数を利用
* **[Keyboard shortcuts](#keyboard-shortcuts)** - コマンド引数を使用したカスタムショートカットを作成、人気のキーマップ拡張機能をメニューからアクセス
* **[JavaScript IntelliSense in HTML](#javascript-language-support-in-html)** - HTML 内の JavaScript 言語サポート
* **[UI for Multitarget Debugging](#multitarget-debugging)** - 複数のデバッグセッション実行
* **[TypeScript 2.1](#typescript-update)** - 最新の TypeScript アップデート採用による言語サポート改善
* **[JavaScript](#javascript)** - Object Rest/Spread サポート

VS Code の重要な更新に関連するアップデート情報は、リリースノートの次のセクションに配置しています。その他のアップデートは、次のとおりです:

* **[Workbench](#workbench)** - 新しいビューピッカー、統合ターミナルの改良、macOS でのウィンドウタイトルテーマ変更設定
* **[Settings](#settings)** - 設定項目の検索、値編集の簡易化、キーマップ拡張機能の検索
* **[Editor](#editor)** - Git Clone(command)、新しいエディタ設定、Sublime Text 機能との互換性
* **[Languages](#languages)** - CSS apply 、Markdown プレビューのカスタマイズ、TSLint と ESLint 拡張機能をアップデート
* **[Debugging](#debugging)** - IntelliSense 介して簡単に launch configurations 設定
* **[Node.js Debugging](#node-debugging)** - Just-My-Code、ファイルから環境変数を読み込み、sourcemap のヘルプ
* **[Extension Authoring](#extension-authoring)** - 厳密な Null チェック、スニペット補完、デバッガ拡張機能の更新

## ワークベンチ (Workbench)

### Hot Exit

`Hot Exit` という機能を新たに追加しました。 VS Code は、以下の時に未保存の変更を記憶します。

- すべてのウィンドウ (インスタンス) が閉じられたとき
- Mac 上で、アプリケーションを終了したとき
- ウィンドウの再読み込みを行ったとき (拡張機能の更新時、未保存を気にする必要がありません)

Hot Exit 後に VS Code を次に起動すると、バックアップされたすべてのワークスペースおよびファイルがリストアされます。 Hot Exitの有効-無効 (`files.hotExit` 設定) に関係なく、VS Code がクラッシュした場合にファイルを復元する機能もあります。Hot Exit の実装や背景および将来の予定などについては、[ブログの記事](http://code.visualstudio.com/blogs/2016/11/30/hot-exit-in-insiders)を参照してください。

### ビューピッカー (View Picker)

ビュー, パネル, 出力チャンネル, ターミナルを表示する新しいピッカーが追加され、隠れているビューを簡単に開くことができるようになりました。 **Open View** コマンドを使用するか、 **Quick Open** 上で `view` を入力したあとに `space` (半角スペース)を入力することで開くことができます。

![View Picker](https://code.visualstudio.com/images/1_8_view-picker.png)

ピッカーを開いたままにします。 `kbstyle(Ctrl)` を保持したまま `kbstyle(Q)` を押すことで項目を選択できます。キーを離したときに選択したビューが開きます。

Windows と Mac では、`kbstyle(Ctrl+Q)` を押すとピッカーを表示します。 Linux は標準でこのコマンドを、アプリケーション終了に割り当てているため、必要に応じて変更をする必要があります。

### 統合ターミナルの改善 (Terminal improvements)

統合ターミナルにいくつかの改良が行われました:

- Windows におけるターミナル上でのコピーと貼り付けのキーバインディングは、それぞれ `kbstyle(Ctrl+C)`（テキストを選択している場合） `kbstyle(Ctrl+V)` に変更されました
- スクロールアップさせている際、ターミナルが出力を受け取っても最下部にスクロールしなくなりました
- ターミナルがフォーカスを持っている場合、`kbstyle(Cmd+K)` によりターミナルをクリアできるようになりました
- 新しい `terminal.integrated.scrollback` 設定により、ターミナル上でスクロールバックを行える行数を設定できるようになりました

### Mac: タイトルバーにもテーマを反映 (Mac: Custom themed title)

macOS 版の VS Code で、テーマのカラーをタイトルバーにも反映できるように、独自のカスタムタイトルバーを内部的に生成するようになりました。この動作は新しい `window.titleBarStyle` 設定で変更することができます。デフォルトは `custom` が設定されていますが、値を `native` に設定し再起動することで従来と同じタイトルバーに変更することができます。

## コードに集中するための機能 (Focus on your code)

今回のリリースで、コーディングへ集中するために役立つ機能を追加しました。

### 禅モード (Zen Mode)

ある[ユーザーからのリクエスト](https://github.com/Microsoft/vscode/issues/12940)により、 VS Code に `禅 (Zen) モード` を追加しました。 Zen モードでは、エディタ以外のすべての UI (アクティビティバー, ステータスバー, サイドバー, パネル)を隠し、フルスクリーン表示にすることでコーディングに集中することができます。

Zen モード切り替えは、**[表示(V)]** -> **コマンド パレット(C)**、 `kbstyle(Ctrl+K Z)` で行います。 Zen モード終了は `kbstyle(Escape)` を2回押します。 Zen モードそのものを無効化したい場合 `workbench.action.toggleZenMode` 設定で変更することができます。

### 設定可能なアクティビティバー (Configurable Activity Bar)
<!-- 英文があまりに回りくどかったので 少し適当 -->
アクティビティバーには、ファイルエクスプローラ, 検索, デバッグなどにアクセスするためのホームがあります。多くの人は、ビューを素早く切り替えたり、ビューに関する情報(例えばGitアイコンではpush時のコミット数を示すバッジ)を表示したりするために使用します。

今回のリリースでは、新機能を追加してアクティビティバーを改善し、アプリケーションドックのような動作をするようになりました。また、これらの設定は VS Code再起動後も保持します。

まず、アクティビティバーそのものを隠すことが可能になりました。 新しく追加された `workbench.activityBar.visible` 設定を使用することで、アクティビティバーを隠すことができます。コマンドでは id `workbench.action.toggleActivityBarVisibility` がこれに当たります。

![Hidden Activity Bar](https://code.visualstudio.com/images/1_8_hide-activitybar.gif)

次に、ビューアイコンをドラック&ドロップでの並び替え、アイコンの表示-非表示(ピン止め)が可能になりました。

![Scalable Activity Bar](https://code.visualstudio.com/images/1_8_viewlet.gif)

VS Codeのウィンドウのサイズが極端に小さくなり全てのビューアイコンを表示できない場合。新しいオーバーフローメニューが追加され、ビューはドロップダウンへ表示されます。

![Scalable Activity Bar](https://code.visualstudio.com/images/1_8_overflow.png)

### タブ上の閉じるボタンを非表示にするための新しい設定 (New setting to hide Close buttons on Tabs)

タブ上の閉じるボタンを非表示にする `workbench.editor.showTabCloseButton` 設定を新たに追加しました。 ダーティー・インジケータ (まだ、ファイルに保存されていないエディタを現すインジケータ)は同一の場所に表示しますが、使用中のタブをマウス操作により誤って閉じることはなくなります。

## 設定 (Settings)
VS Code の設定変更は `settings.json` ファイルを編集する形式となり、非常に簡単な操作で動作を設定することが可能です。ユーザーが使用可能な設定を見つけるために、**既定の設定** を別のエディタで表示し、グローバルまたはワークスペース設定をもう1つのエディタで開き、IntelliSense による設定を行ってきました。

しかし、ユーザーからのフィードバックとユーザビリティの調査から、この方法は問題であることが判明しました。

今回のリリースでは、設定項目を探す方法の可能性とユーザーエクスペリエンスを向上させるためのいくつかの調査を行った結果、次のような改善をしました。

### 設定の検索 (Search settings)

**既定の設定** を表示する大きな理由の1つは、ユーザーが設定を検索及び検出するためです。これを容易にするために、設定を検索できる大きな検索バーを追加しました。検索に一致する設定の強調表示に加えて、一致しない設定を除外します。これにより、設定を素早く簡単に見つけることができます。<!--text lint無視-->

![Search Settings](https://code.visualstudio.com/images/1_8_search-settings.gif)

### 設定グループ (Settings groups)

**既定の設定** グループの視覚的表現を強化し、設定のナビゲーションをより使いやすくしました。また、`最もよく利用するもの`を表示するグループを追加しました。

![Settings Groups](https://code.visualstudio.com/images/1_8_settings-groups.png)

### クイックエディット (Quick Edit)

**既定の設定** と `settings.json` エディタ内で、設定をすばやくコピーまたは更新するのに役立つアクションを導入しました。あらかじめ選択可能な値を持っている項目については、値をキーボードから入力することなく選択で入力することが可能です。

![Settings Groups](https://code.visualstudio.com/images/1_8_quick-edit-settings.gif)

### 設定エディタのグループ化 (One Side by Side Settings editor)

紹介が最後になりましたが、これも重要な改善になります。 **既定の設定** と `settings.json` エディタをサイドエディタでグループ化することにより、2つの設定用エディタを個別に管理しなければならなかった問題に対処しました。

エディタには様々な改善が続けられて行きます...次のリリース計画に注目してくださいね

## キーボードショートカット (Keyboard shortcuts)

### キーバインディングコマンドの引数 (Key binding command arguments)

`keybindings.json` 設定ファイルにて、引数を持つコマンドを呼び出すためのサポートを追加しました。これは、特定のファイルやフォルダに対して同じ操作を繰り返し実行する場合などに便利な機能となります。カスタムキーボードショートカットを追加するだけで、必要な操作を正確に実行できます。

以下は、`kbstyle(Enter)` の入力によりテキスト `Hello World` を表示するように、既存の `kbstyle(Enter)` キーを上書きする例です：

```json
  { "key": "enter", "command": "type",
                    "args": { "text": "Hello World" },
                    "when": "editorTextFocus" }
```

`"command": "type"` により、`kbstyle(Enter)` キーが入力されると `{"text"： "Hello World"}` を最初の引数として受け取り、"Hello World" をエディタに出力する動作となります。

### 推奨されるキーマップ拡張 (Recommended keymap extensions)

一般的なエディタや IDE で採用されているフルセットのキーバインディングを VS Code でも利用可能になるキーマップ拡張機能リストを表示するコマンドを追加しました。

リストを表示するには、**[ファイル(F)]** > **基本設定(P)** > **キーマップ拡張機能(K)** を使用します。

![Recommended keymap extensions](https://code.visualstudio.com/images/1_8_recommended-keymap-extensions.png)

## エディタ (Editor)

### 選択範囲メニューの追加 (Selection menu)

メニューバーに **[選択範囲(S)]** メニューを追加し、良く利用される選択操作と複数選択操作に容易にアクセスできるようになりました。 <!--text lint無視-->

![Selection menu](https://code.visualstudio.com/images/1_8_selection-menu.png)

### テキスト検索のパフォーマンス向上 (Text search performance)

複数のプロセスで検索コードを並行して実行することにより、フルテキスト検索の[パフォーマンス](https://github.com/Microsoft/vscode/issues/15384)を向上しました。 特に大規模なワークスペースでは、検索がより高速に完了するはずです。

### Git clone

Git リポジトリをクローンし、VS Code で開くための新しいコマンドを追加しました。**コマンド パレット** から、`Git：Clone` を検索することで実行することができます。

### 新しく追加されたエディタ設定 (New editor settings)

* `window.showFullPath` - ウィンドウタイトルに、ワークスペースの相対パスではなく、開いているファイルのフルパスを表示します
* `files.insertFinalNewline` - ファイル保存時、ファイルの最後に改行を自動的に追加します

`editor.renderLineHighlight` 設定に新しいオプションを追加しました:

* `line` - エディタで現在の行をハイライト表示する
* `gutter` - 現在の行の左側にあるガターの行番号をハイライト表示する
* `all` - ガターとラインの両方をハイライト表示する
* `none` - 現在の行をハイライト表示しない

![render line highlight](https://code.visualstudio.com/images/1_8_render-line-highlight.png)

### diff エディタのアクセシビリティを向上 (Accessibility improvements of diff editor)

diff エディタに変更をあらわす `+` と `-` のインジケータを追加することで、diff エディタのアクセシビリティを強化しました。この機能はデフォルトで有効ですが、`diffEditor.renderIndicators` を `false` に設定することで無効にすることもできます。

![diff indicators](https://code.visualstudio.com/images/1_8_diff-indicators.png)

### Sublime Text との互換性 (Sublime Text compatibility)

Sublime Text ユーザーがよく利用する 4 つの新しいコマンドを追加しました。

- 行をつなげる (Join Lines) - `editor.action.joinLines`
- カーソルの周囲の文字列を入れ替える (Transpose characters around the cursor) - `editor.action.transpose`
- 大文字に変換 (Transform to Uppercase) - `editor.action.transformToUppercase`
- 小文字に変換 (Transform to Lowercase) - `editor.action.transformToLowercase`

これらのコマンドは、デフォルトではキーボードショートカットにバインドされていませんが、**コマンド パレット** から呼び出すことも可能です。

## スニペット (Snippets)

### スニペット変数 (Snippet Variables)

カスタムスニペットで、変数を使用できるようになりました。 変数の構文は、単純な変数の場合は `$name` となり、デフォルト値を持つ変数の場合は `${name:default}` のようになります。変数の中が空の文字列、または値が存在する場合は、それらがデフォルト値として評価します。変数が不明な場合は、その変数をプレースホルダとして挿入します。

次の変数を使用できます:

* `TM_SELECTED_TEXT` - 現在選択しているテキストまたは空の文字列
* `TM_CURRENT_LINE` - 現在の行の内容
* `TM_CURRENT_WORD` - カーソルが置かれている単語の内容または空の文字列
* `TM_LINE_INDEX` - zero-index に基づく行番号
* `TM_LINE_NUMBER` - one-index に基づく行番号
* `TM_FILENAME` - 現在のドキュメントのファイル名
* `TM_DIRECTORY` - 現在のドキュメントのディレクトリ
* `TM_FILEPATH` - 現在のドキュメントの完全なファイルパス

以下は、選択したテキストをシングルクォートで囲むスニペットの例です。テキストを選択していない場合は、`type_here`-プレースホルダが挿入されます。

```json
"in quotes": {
	"prefix": "inq",
	"body": "'${TM_SELECTED_TEXT:${1:type_here}}'"
}
```

### JSON スキーマのスニペット (Snippets in JSON schemas)

JSON 言語サービスでは、JSON スキーマを使用して JSON ドキュメントの検証と補完を行います。JSON スキーマにおける。VS Code 固有機能で、利便性を向上するためにスキーマへのスニペット提案を指定できるようになりました。スニペットの提案は追加の補完提案として表示され、スニペット構文を使用してプレースホルダを指定します。

詳細については、[JSON ドキュメント](https://code.visualstudio.com/docs/languages/json#_json-schemas-settings)を参照してください。

## Languages

### HTML での JavaScript 言語サポート (JavaScript language support in HTML)

HTML に埋め込まれた JavaScript のコーディング支援機能が復活しました！コード補完、DOM の署名ヘルプ、JQuery API、検証、ホバー、参照の検索と定義への移動、シンボルの強調表示と概要 (Ctrl + Shift + o)、フォーマットなどの機能を利用できます。この言語サポートは同じファイル内の定義のみで有効なことに注意してください。

![JavaScript editing in HTML](https://code.visualstudio.com/images/1_8_javascript-in-html.gif)

### CSS の改善 (CSS improvements)

CSS 言語サポートでは、新しい [@apply ルール](https://tabatkins.github.io/specs/css-apply-rule/) を処理できるようになりました。

特に属性で定義されたスタイルを持つ HTML での CSS サポートを改善しました。

![CSS in HTML attributes](https://code.visualstudio.com/images/1_8_css-in-html.png)

### TypeScript Update

JavaScript と TypeScript 言語サポートに [TypeScript 2.1](https://blogs.msdn.microsoft.com/typescript/2016/12/07/announcing-typescript-2-1/) を採用しています。 TypeScript 2.1 は、多くの新しい言語機能とツーリング機能を提供しています。詳細は、[TypeScript 2.1 の新機能について](https://github.com/Microsoft/TypeScript/wiki/What's-new-in-TypeScript#typescript-21)を参照してください。

### JavaScript

VS Code における JavaScript サポートは TypeScript によって強化されています。また、VS Code には最新の TypeScript バージョンがバンドルされ、JavaScript サポートのためのいくつかの改良が施されています:

* [Object Rest と Spread のサポート](https://github.com/Microsoft/TypeScript/wiki/What's-new-in-TypeScript#object-spread-and-rest)。これは React を利用している JS 開発者から要望の多いリクエストでした。Object Spread/Rest を使用する際、JavaScript の検証を無効にする必要はなくなりました。
* jsconfig.json ファイル[構成の継承](https://github.com/Microsoft/TypeScript/wiki/What's-new-in-TypeScript#configuration-inheritance)
* IntelliSense による `import` および `require` に必要なパスの補完

### Markdown プレビューの改善 (Markdown preview improvements)

Markdown プレビューを改善するためのいくつかの新しい設定を追加しました。

* `markdown.previewFrontMatter` - デフォルトの動作として、Markdown プレビュー時に YAML front matter セクションを隠すようになりました。YAML front matter もあわせてプレビュー上で確認したい場合は `show` に設定してください

Markdown プレビューで使用するフォントファミリ、サイズ、行の高さを制御します。

* `markdown.preview.fontFamily`
* `markdown.preview.fontSize`
* `markdown.preview.lineHeight`

### リンター拡張機能 (Linter Extensions)

#### vscode-tslint

vscode-tslint 拡張機能が [TSLint 4.0](https://palantir.github.io/tslint/2016/11/17/new-for-4.0.html) をサポートしました。TSLint 4.0 では、警告関するクイックフィックスや JavaScript ファイルのリンティングのサポートが追加されています。さらに、`vscode-tslint` で、次の行の TSLint ルールを無効にするためのクイックフィックスを追加しました。 TSLint のアップデート詳細については [CHANGELOG](https://github.com/Microsoft/vscode-tslint/blob/master/tslint/CHANGELOG.md) を参照してください。

#### vscode-eslint

`vscode-eslint` 拡張機能は、JavaScript 以外のファイルタイプの検証をサポートしました。この機能を有効化するには、次の操作が必要です:

- 検証を有効化するには、追加のプラグインを使用して ESLint を設定する必要があります。たとえば、HTML ファイルを検証するには、まず、`npm install eslint-plugin-html` を実行し、`eslint-plugin-html` インストールします。その後、eslint 設定ファイル (.eslintrc.jsonファイル) に `"plugin": [ "html" ]` を追加します
- さらに、対応する言語識別子を `"eslint.validate": [ "javascript", "javascriptreact", "html" ]` のように `eslint.validate` 設定に追加します。この設定がされない場合のデフォルト値は `["javascript", "javascriptreact"]` となります。

## デバッグ (Debugging)

### マルチターゲットデバッグ (Multitarget debugging)

マルチターゲットデバッグは、以前のマイルストーンで実装されました。今回のマイルストーンでは、新たにユーザインタフェースを追加し、マルチターゲットデバッグはもはや実験的な機能ではなくなりました。

マルチターゲットデバッグの使用は非常に簡単です: 最初のデバッグセッションを開始した後、別のセッションの起動をブロックすることはなくなり、2 つ目のセッションを起動することで UI が _multi-target mode_ に切り替わります:

- 個々のデバッグセッションは、CALL STACK ビューのトップレベル要素として表示されるようになりました。
![Callstack View](https://code.visualstudio.com/images/1_8_debug-callstack.png)
- フローティングデバッグウィジェットは、現在アクティブなデバッグセッションを表示します (他すべての稼働しているセッションには、ドロップダウンメニューから選択可能です)
![Debug Actions Widget](https://code.visualstudio.com/images/1_8_debug-actions-widget.png)
- デバッグアクション(たとえば、フローティングデバッグウィジェットのすべてのアクション)は、アクティブセッションで実行されます。アクティブセッションの切り替えは、フローティングデバッグウィジェットのドロップダウンメニューから選択するか、CALL STACK ビューで対象となる要素を選択して変更することができます。
- セッションが停止するたびに(たとえば、ブレークポイントまたは例外がヒットしたときなど)、そのセッションは、アクティブなセッションに切り替わり、'F5' キーを押すだけで簡単にデバッグセッションを開始することができます。

複数のデバッグセッションを開始する別の方法として提供されるのが、_compound_ launch configuration を使用する方法です。_compound_ launch configuration を実現するには、並列に起動する 2 つ以上の起動構成の名前をリストする必要があり、launch configuration ドロップダウンメニューに表示されます。

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "type": "node",
            "request": "launch",
            "name": "Server",
            "program": "${workspaceRoot}/server.js",
            "cwd": "${workspaceRoot}"
        },
        {
            "type": "node",
            "request": "launch",
            "name": "Client",
            "program": "${workspaceRoot}/client.js",
            "cwd": "${workspaceRoot}"
        }
    ],
    "compounds": [
        {
            "name": "Server/Client",
            "configurations": ["Server", "Client"]
        }
    ]
}
```

この [blog](https://medium.com/@auchenberg/introducing-simultaneous-nirvana-javascript-debugging-for-node-js-and-chrome-in-vs-code-d898a4011ab1#.fehi3batj) では、Node.js バックエンドとブラウザフロントエンドの複合設定を構成する方法について詳しく説明しています。

### 個々の起動構成の追加 (Adding individual Launch Configurations)

IntelliSense によるスニペット候補の選択をサポートすることで、既存の `launch.json` へ新しい設定を追加する操作をより便利にできないか検討しました。
IntelliSense によるスニペットの呼び出しは、カーソルが `configurations` アレイ内にある場合に使用できるほか、**Add Configuration** ボタンを押して、IntelliSense を呼び出し、スニペットをアレイの先頭に挿入することも可能です。

![Add Configuration](https://code.visualstudio.com/images/1_8_add-config.gif)

インストールされたすべてのデバッグ拡張機能で提供される起動設定スニペットが IntelliSense により一覧表示されます。これにより、さまざまなデバッガ (Chrome や Node など)の起動設定を 1 つの `launch.json` として簡単に組み合わせることが可能になります。

デバッグ拡張機能は、この新機能の採用を選択する必要があり、すべてのデバッガがこの機能を利用できるまでは、しばらく時間を必要とします。VS Code 11月 リリースでは、ビルトインの Node.js デバッガだけが利用可能です。

### 洗練されたいくつかのユーザインタフェース (Some UI Polish)

[ユーザーのリクエスト](https://github.com/Microsoft/vscode/issues/14125) により、ドラッグアンドドロップによってウォッチ式の順序を並べ替えることが可能になりました。

また、スタートボタンとドロップダウンメニューをグループ化することにより、デバッグ開始アクションUIの外観を洗練させました:

![DebugStart](https://code.visualstudio.com/images/1_8_debug-start.png)

BREAKPOINTS ビューに表示されるソースと行番号情報は、CALL STACK ビューの情報に合わせ、より良く整列するように再配置されます。

![Breakpoints](https://code.visualstudio.com/images/1_8_breakpoints.png)

## Node.js のデバッグ (Node Debugging)

このセクションでは、VS Code に組み込まれている 2つの Node.js デバッガである `node` および `node2` の機能について説明します。これら 2 つのデバッガで同等の機能を維持しようと試みていますが、新しいテクノロジ (_Chrome Debugger Protocol_) が急速に進化するのに対して、`node` (_V8 Debugger Protocol_)の技術が非推奨(事実上、開発が凍結)となったため、ますます難しくなっています。このような理由から、我々は、各機能のヘッダの括弧内にサポートされているデバッガのタイプをリストします。

Node.js バージョンが 6.3 より古い場合は、`古い`デバッガである `node` を使用し、6.3 または、より新しいバージョンを利用する場合は、新しいデバッガとなる `node2` を使用します。

>**Note:** Node.js アプリケーションで ES6 Proxy を使用している場合、古いデバッガで Node.js v7.x 実行環境をデバッグするとクラッシュする可能性があります。 これは、新しいデバッガ `node2` では発生しません。この問題は、 [Microsoft/vscode#12749](https://github.com/Microsoft/vscode/issues/12749) で調査されています

### "マイ コードのみ" (Just My Code (node and node2))

ステップ実行したくないコードを回避するための機能が追加されました。これは、Visual Studio でも提供される [Just My Code](https://msdn.microsoft.com/ja-jp/library/dn457346.aspx) に良く似た機能です。
この機能は、起動設定の `skipFiles` 設定で有効にすることができ、`skipFiles` はスキップするスクリプトパスのグロブパターン配列を設定します。

使用例:

```typescript
  "skipFiles": [
    "node_modules/**/*.js",
    "lib/**/*.js"
  ]
```

この設定では、`node_modules` および `lib` フォルダ内に配置される全てのコードがスキップされます。

正確なルールは次のとおりです:

* スキップ対象となるファイルにステップインした場合、そこで停止することはありません。スキップされたファイルにない次の実行されたラインで停止します
* スローされた例外を破棄するオプションを設定した場合、スキップ対象となるファイルからスローされた例外が中断されることはありません
* スキップ対象となるファイルにブレークポイントを設定した場合、そのブレークポイントで停止し、そのブレークポイントからステップアウトするまでステップを進めることができます。このポイントから通常のスキップ動作が再開されます。

この機能は、`node`、 `node2` および [Chrome](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome) デバッガで使用できます。

>**Note:** 古いデバッガ (`node`) はネガティブグロブパターンをサポートしていますが、ポジティブパターンに**従わなければなりません**: ポジティブパターンはスキップ対象となるファイルのセットに追加され、ネガティブパターンはそのセットから削除されます。

次の例では、'math' モジュールを除くすべてのモジュールがスキップされます:

```typescript
"skipFiles": [
    "node_modules/**/*.js",
    "!node_modules/math/**/*.js"
]
```

>**Note:** 古いデバッガ (`node`) では、_V8 Debugger Protocol_ をネイティブにサポートしていないため、_Just My Code_ 機能をエミュレートする必要があります。そのため、ステッピング実行が遅くなる可能性があります。


### 外部ファイルから環境変数をロード (node) (Load environment variables from external file (node))

VS Code の Node デバッガは、ファイルから環境変数をロードし Node ランタイムに渡す機能をサポートしました。
この機能を使用するには、`envFile` 属性を launch configration に追加し、環境変数を含むファイルへの絶対パスを指定します:

```typescript
   //...
   "envFile": "${workspaceRoot}/.env",
   "env": { "USER": "john doe" }
   //...
```

`env` ディクショナリで指定された環境変数は、ファイルからロードされた変数を上書きします。

'.env'ファイルの例は次のようになります:

```yaml
USER=doe
PASSWORD=abc123

# a comment

# an empty value:
empty=

# new lines expanded in quoted strings:
lines="foo\nbar"
```

### ソースマップの問題診断（node2）(Diagnostics for Source Map Problems (node2))

Node.js アプリケーションをデバッグすると、"Source map problem?" というメッセージが表示され、ブレークポイントがグレーになっていることがあります。 このような問題を理解しやすくするために、新しい `node2` デバッグアダプタでは 2 つの新機能を提供します。

デバッグセッション中、デバッグコンソールに `.scripts` と入力することで、アダプタは、ロードされたスクリプトとその sourcemap に関するすべての情報を出力します。

また、起動設定の `sourceMapPathOverrides` オプションを使用すると、デバッグアダプタがディスク上の正しいソースファイルを見つけるのに十分な情報が sourcemap ファイルに含まれていない場合に、sourcemap ファイル内のパスを書き換えることが可能です。これらの機能の詳細については、[`node2` README](https://github.com/Microsoft/vscode-node-debug2#the-scripts-command) を参照してください。

### 時間を遡ったデバッグ (Back in time Debugging (node))

この UI は、Chakra ベースの Node.js ランタイムを利用している場合に限り自動的に表示されます。 詳細は[このブログ](https://blogs.windows.com/msedgedev/2016/11/29/node-chakracore-vm-neutrality/#cr7wJLzUhp37TVcI.97)を参照してください。

`node` デバッガの `Reverse Continue` アクションを拡張することにより、_Back In Time Debugging_ をサポートしています。

![Reverse Continue](https://code.visualstudio.com/images/1_8_reverse-continue.png)

## 拡張機能のオーサリング (Extension Authoring)

### 厳密な Null チェックサポート (Strict Null Checks supported)

型が `undefined` (未定義) または `null` の場合、明示的に記入しなければならないよう `vscode.d.ts` の型定義をアップデートしました。このアップデートは、より良い型チェックを得るために、TypeScript の `strictNullChecks`-feature を利用しています。

### スニペット補完候補 (Snippet Completions)

completion item プロバイダは、スニペットとして挿入された補完候補を返すようになりました。 アイテムを作成するときは、`insertText` が [`SnippetString`](https://github.com/Microsoft/vscode/blob/master/src/vs/vscode.d.ts#L2073) であることを確認してください。 これを選択すると、エディタはスニペットモードに移行し、プレースホルダとカーソル位置を制御できます。

### 構成の検査 (Inspect Configurations)

新しい [`inspect`](https://github.com/Microsoft/vscode/blob/master/src/vs/vscode.d.ts#L2825)-function を利用することで、設定値やデフォルト値の定義箇所を知ることが可能になります。

### TextDocument#getWordRangeAt

text document では、指定された位置からの [word-range](https://github.com/Microsoft/vscode/blob/master/src/vs/vscode.d.ts#L221) (単語の範囲)を得ることができます。 VS Code は、どのような単語かを知るために、それぞれの言語の [word-pattern](https://github.com/Microsoft/vscode/blob/master/src/vs/vscode.d.ts#L2714) (単語パターン)を使用しますが、それだけでは十分ではないため、代替として使用される正規表現を提供できるようになりました。

### デバッガ拡張機能のオーサリング (Debugger Extension Authoring)

`launch.json` における、トップレベルの `debugServer` 属性が廃止されました (サポートは、2月のマイルストーンで削除される予定です)。代わりに、`debugServer` 属性を起動設定ごとに指定する必要があります。 詳細については、[こちら](https://github.com/Microsoft/vscode/issues/13783)で確認してください。

デバッガ拡張機能は、`launch.json` で launch configuration スニペットを提供するようになりました。詳細については、"個々の起動設定の追加" を参照してください。

 これは VS Code でスニペットを提供するために利用される通常の構文を使用して行うことができますが、`package.json` の `debuggers` セクション内の `configurationSnippets` 属性にスニペットを記述することも可能です。Mock Debug がデバッグ設定スニペットにどのように設定しているかの例は、[ここを参照](https://github.com/Microsoft/vscode-mock-debug/blob/master/package.json#L71)してください。

### VS Code Debug Protocol

`OutputEvent` タイプは、構造化オブジェクトをデバッグコンソールに送信する機能としてサポートされ、VS Code で拡張オブジェクトとしてレンダリングされるようになりました。詳細は[こちら](https://github.com/Microsoft/vscode-debugadapter-node/issues/79)をご覧ください。

新しい `RestartRequest` をデバッグプロトコルに追加しました。VS Code デバッガ UI に、デバッグアダプタを終了および再起動する `Restart` アクションの実装が必要なくなり、代わりに `RestartRequest` をアダプタに送信します。 詳細は[こちら](https://github.com/Microsoft/vscode/issues/14189)をご覧ください。

## その他 (Miscellaneous)

### Electron のアップデート (Electron update)

今回のリリースでは、Electron を 1.3.x から 1.4.x にアップデートしました。これにより、Chrome はバージョン 52 から 53 へアップデートされます。また、このアップデートによりは、100％ 以上の DPI で VS Code が動作している場合、Windows におけるフォントレ(タリング?)表示のぼやけが軽減されるとユーザーから報告を受けています。

アップデートのもう1つの利点として、 Windows が高コントラストモードで動作していることを検出したとき、高コントラストテーマを自動で有効にできることです。起動中でもWindows でモードを変更するとハイコントラストモードに切り替わります。

### Language Server Protocol

LSP でも VS Code API と同様に、全てのアイテムをスニペットでサポートされるようになりました。さらに、クライアント側でプロバイダの動的登録をサポートするための 2 つの新しいリクエストが導入されています。また、LSP NPM Node モジュールは、TypeScript 2.0 にアップグレードされました。 詳細については、[https://github.com/Microsoft/language-server-protocol](https://github.com/Microsoft/language-server-protocol) および [https://github.com/Microsoft/vscode-languageserver-node](https://github.com/Microsoft/vscode-languageserver-node) を参照してください。

## 新しく追加されたコマンド (New Commands)

> **NOTE**: プラットフォームによってキーの表記が変わりますので、テーブルの内容については、<https://code.visualstudio.com/updates#_new-commands> にて確認してください。

Key|Command|Command id
---|-------|----------
`kb(workbench.action.quickOpenView)`|Quick Open ビュー (Quick Open View)|`workbench.action.quickOpenView`
`kb(workbench.action.nextEditorInGroup)`|グループ内で次のエディタを開く (Open Next Editor in Group)|`workbench.action.nextEditorInGroup`
`kb(workbench.action.previousEditorInGroup)`|グループ内で前のエディタを開く (Open Previous Editor in Group)|`workbench.action.previousEditorInGroup`
`kb(workbench.action.toggleZenMode)`|Zen Mode の切り替え (Enable Zen Mode)|`workbench.action.toggleZenMode`
`kb(workbench.action.exitZenMode)`|Leave Zen Mode|`workbench.action.exitZenMode`
`kb(workbench.action.closePanel)`|Close active Panel|`workbench.action.closePanel`
`kb(workbench.action.git.clone)`|Clone from a Git URL|`workbench.action.git.clone`
`kb(workbench.action.toggleActivityBarVisibility)`|Toggle Visibility of Activity Bar|`workbench.action.toggleActivityBarVisibility`
`kb(workbench.action.quit)`|Quit VS Code|`workbench.action.quit`
`kb(editor.action.joinLines)`|Join Lines|`editor.action.joinLines`
`kb(editor.action.transpose)`|Transpose characters around the cursor|`editor.action.transpose`
`kb(editor.action.transformToUppercase)`|Transform to Uppercase|`editor.action.transformToUppercase`
`kb(editor.action.transformToLowercase)`|Transform to Lowercase|`editor.action.transformToLowercase`

## 重要な変更 (Notable Changes)

* [16330](https://github.com/Microsoft/vscode/issues/16330): Use cached data to speed up script parsing
* [16065](https://github.com/Microsoft/vscode/issues/16065): First https request is responsible for 18% of windows startup time
* [15111](https://github.com/Microsoft/vscode/issues/15111): External file watcher fails for editors that do atomic saves
* [14951](https://github.com/Microsoft/vscode/issues/14951): Download vscode very slow in China
* [13104](https://github.com/Microsoft/vscode/issues/13104): Windows: selected tree item not accessible
* [13527](https://github.com/Microsoft/vscode/issues/13527): Text is super blurry now
* [15741](https://github.com/Microsoft/vscode/issues/15741): Allow code to open directories in nautilus file manager

[クローズされたバグ一覧](https://github.com/Microsoft/vscode/issues?q=is%3Aissue+label%3Abug+milestone%3A%22November+2016%22+is%3Aclosed)と、1.8 アップデートにて[クローズされた機能のリクエスト一覧](https://github.com/Microsoft/vscode/issues?q=is%3Aissue+milestone%3A%22November+2016%22+is%3Aclosed+label%3Afeature-request)です。

## 拡張機能への貢献 (Contributions to Extensions)

私たちのチームは、いくつかの VS Code 拡張機能の提供とメンテナンスに貢献しています。注目すべき拡張機能は：

* [Go](https://marketplace.visualstudio.com/items?itemName=lukehoban.Go)
* [Python](https://marketplace.visualstudio.com/items?itemName=donjayamanne.python)
* [TSLint](https://marketplace.visualstudio.com/items?itemName=eg2.tslint)
* [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
* [Debugger for Chrome](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome)
* [VSCodeVim](https://marketplace.visualstudio.com/items?itemName=vscodevim.vim)
* [Mono Debug](https://marketplace.visualstudio.com/items?itemName=ms-vscode.mono-debug)
* [Mock Debug](https://marketplace.visualstudio.com/items?itemName=andreweinand.mock-debug)

## Thank You

最後になりましたが、VS Code をより良いものへするために協力してくれた次の方々に多大なる感謝を込めて:

* [@anantoghosh](https://github.com/anantoghosh):  Fix Incorrect links in "vscode namespace API" Doc [PR #15904](https://github.com/Microsoft/vscode/pull/15904)
* [Christian Alexander (@ChristianAlexander)](https://github.com/ChristianAlexander):  Fix #14135 - Allow files with merge status to be staged [PR #14788](https://github.com/Microsoft/vscode/pull/14788)
* [Faustino Aguilar (@faustinoaq)](https://github.com/faustinoaq):  Support HTML comments in Markdown [PR #14573](https://github.com/Microsoft/vscode/pull/14573)
* [Felix Becker (@felixfbecker)](https://github.com/felixfbecker)
  *  Repl links fix [PR #15174](https://github.com/Microsoft/vscode/pull/15174)
  *  Improve REPL link highlight regexp [PR #15406](https://github.com/Microsoft/vscode/pull/15406)
  *  Only resolve paths in REPL if path is relative [PR #15794](https://github.com/Microsoft/vscode/pull/15794)
  *  Resolve relative REPL paths [PR #15464](https://github.com/Microsoft/vscode/pull/15464)
* [Sanders Lauture (@golf1052)](https://github.com/golf1052):  Provide an option to hide the activity bar [PR #14940](https://github.com/Microsoft/vscode/pull/14940)
* [Huachao Mao (@Huachao)](https://github.com/Huachao)
  *  Add .conf and .cfg file extensions for ini language [PR #15512](https://github.com/Microsoft/vscode/pull/15512)
  *  Add Translation Memory eXchange (TMX) support [PR #14894](https://github.com/Microsoft/vscode/pull/14894)
* [Michael Hudson (@Huddo121)](https://github.com/Huddo121):  Add tests for zoom level functionality [PR #14737](https://github.com/Microsoft/vscode/pull/14737)
* [Yuichi Tanikawa (@itiut)](https://github.com/itiut):  Add .zsh-theme to shellscript extensions [PR #15489](https://github.com/Microsoft/vscode/pull/15489)
* [Kai Wood (@kaiwood)](https://github.com/kaiwood):  Fix focus and configuration handling of the integrated terminal [PR #15958](https://github.com/Microsoft/vscode/pull/15958)
* [Matt King (@KattMingMing)](https://github.com/KattMingMing):  Support opening files through URL handling (fixes #4883) [PR #15320](https://github.com/Microsoft/vscode/pull/15320)
* [Jonathan Carter (@lostintangent)](https://github.com/lostintangent):  Adding Docker 1.12 instructions to its grammar [PR #16476](https://github.com/Microsoft/vscode/pull/16476)
* [Pine (@octref)](https://github.com/octref):  Declarative contribution of custom Tree Explorer [PR #14048](https://github.com/Microsoft/vscode/pull/14048)
* [Munir Mastalic (@polygotdev)](https://github.com/polygotdev):  add conditional to rpm spec to test for arch, fixes 13616 [PR #15128](https://github.com/Microsoft/vscode/pull/15128)
* [scheakur (@scheakur)](https://github.com/scheakur):  Remove duplicate test code [PR #16061](https://github.com/Microsoft/vscode/pull/16061)
* [Sean Kelly (@xconverge)](https://github.com/xconverge):  fixes #16553 [PR #16689](https://github.com/Microsoft/vscode/pull/16689)
* [Yuya Tanaka (@ypresto)](https://github.com/ypresto):  Fix backslash is not escaped by define key binding [PR #16108](https://github.com/Microsoft/vscode/pull/16108)
* [Tamas Kiss (@kisstkondoros)](https://github.com/kisstkondoros):  Standardize cursor movement with home and end keys [PR #17027](https://github.com/Microsoft/vscode/pull/17027)

`vscode-tslint` への貢献:

* [Eric Anderson (@ericanderson)](https://github.com/ericanderson):  Detect 4.0.0 for -dev versions of TSLint [PR #141](https://github.com/Microsoft/vscode-tslint/pull/141)
* [Richard Lasjunies (@rlasjunies)](https://github.com/rlasjunies): fix most of the autoFix issues using TSLint 4.0 [PR #138](https://github.com/Microsoft/vscode-tslint/pull/138)
* [Robert Stoll (@robstoll)](https://github.com/robstoll):  reverts #107, seems like rule name was removed [PR #140](https://github.com/Microsoft/vscode-tslint/pull/140)
* [Yuichi Nukiyama (@YuichiNukiyama)](https://github.com/YuichiNukiyama)
  *  backward compatibility for js files [PR #137](https://github.com/Microsoft/vscode-tslint/pull/137)
  *  support .jsx file [PR #126](https://github.com/Microsoft/vscode-tslint/pull/126)
  *  Support javascript files [PR #120](https://github.com/Microsoft/vscode-tslint/pull/120)

`vscode-debugadapter-node` への貢献:

* [Richard Stanton (@richardstanton)](https://github.com/richardstanton): Allow requests to specify formatting hints. [PR #82](https://github.com/Microsoft/vscode-debugadapter-node/pull/82)

`language-server-protocol` への貢献:

* [Vlad Dumitrescu (@vladdu)](https://github.com/vladdu):
  * add link to JSON-RPC specification [PR #123](https://github.com/Microsoft/language-server-protocol/pull/123)
  * add table of contents to the specification [PR #117](https://github.com/Microsoft/language-server-protocol/pull/117)
* [Guillaume Martres (@smarter)](https://github.com/smarter): Correct minor issue in ParameterInformation doc [PR #108](https://github.com/Microsoft/language-server-protocol/pull/108)
* [Peter Burns (@rictic)](https://github.com/rictic): [minor] Fix a couple [PR #103](https://github.com/Microsoft/language-server-protocol/pull/103)

`vscode-languageserver-node` への貢献:

* [CJ Bell (@siegebell)](https://github.com/siegebell): CancellationToken.is does not check for undefined [PR #121](https://github.com/Microsoft/vscode-languageserver-node/pull/121)
* [Gama11 (@Gama11)](https://github.com/Gama11): Typo fix: "hove" -> "hover" [PR #109](https://github.com/Microsoft/vscode-languageserver-node/pull/109)

`vscode-css-languageservice` への貢献:

* [Denis Malinochkin (@mrmlnc)](https://github.com/mrmlnc):
  * Support !important in Variables [PR #3](https://github.com/Microsoft/vscode-css-languageservice/pull/3)
  * Display value of Variable [PR #14](https://github.com/Microsoft/vscode-css-languageservice/pull/14)
  * Add Mixin proposals [PR #17](https://github.com/Microsoft/vscode-css-languageservice/pull/17)
* [Peter Burns (@rictic)](https://github.com/rictic):
  * Fully support parsing Custom Property values [PR #11](https://github.com/Microsoft/vscode-css-languageservice/pull/11)
  * Add support for parsing @apply rules. [PR #10](https://github.com/Microsoft/vscode-css-languageservice/pull/10)