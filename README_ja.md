![](https://github.com/fastai/nbdev/workflows/CI/badge.svg)


# nbdev へようこそ
> Jupyter Notebooks を使用して楽しい python プロジェクトを作成します

`nbdev` は 完全に [Jupyter Notebooks](https://jupyter.org/) で開発した、すべてのコード、テスト、ドキュメントを1か所にまとめることができるライブラリです。つまり、1983年にドナルド・クヌースが思い描いていたように、本当の意味での [文芸的プログラミング](https://en.wikipedia.org/wiki/Literate_programming)環境が手に入りました。

インタラクティブ環境を使用すると、コードを簡単にデバッグしてリファクタリングできます。あなたの Pythonモジュールに含めたい関数を定義するセルに、`#export` フラグを追加します。ここでは、たとえば、`fastai` ライブラリで `combined_cos` がでどのように定義および文書化されているかを示します。

<img alt="Exporting from nbdev" width="700" caption="An example of a function defined in one cell (marked with the export flag) and explained, along with a visual example, in the following cells" src="nbs/images/export_example.png">

このように記述されたノートブックを使用すると、`nbdev` は、1つのコマンドで次のいずれかを作成して実行できます。

- 検索可能なハイパーリンクされたドキュメント; バッククォートで囲む単語は、適切なドキュメントに *自動的に* ハイパーリンクされます。
- Pythonモジュール、エクスポートされた関数、クラス、変数を使用して自動的に定義する `__all__` （[詳細](http://xion.io/post/code/python-all-wild-imports.html)）
- Pip インストーラー （pypi にアップロードされます）
- テスト（ノートプックで直接定義され、並行して実行されます）
- 標準のテキストエディターまたはIDEでコードを操作・編集し、ノートブックに対して自動的に変更内容をエクスポートします。

ノートブックを使用しているため、あなたのライブラリのドキュメントに含まれる、グラフ、テキスト、リンク、画像、ビデオなどを自動的に追加することもできます。コードが定義されているセルは非表示になり、関数の名前、引数、docstring、および github 上のソースコードへのリンクなど、関数の標準化されたドキュメントに置き換えられます。たとえば上記のセルは、次のように変換されます：

<img alt="Documentation in nbdev" width="600" caption="An example of automated documentation from the fastai library" src="nbs/images/doc_example.png">

*インストール* と *入門* については、以下を参照してください。ドキュメントの他のページでは、次の詳細を取得できます:

- jupyter notebooks から pythonライブラリに[export](http://nbdev.fast.ai/export)する機能
- [cli](http://nbdev.fast.ai/cli) コマンドはターミナルで nbdev を使用することができます
- [export2html](http://nbdev.fast.ai/export2html) がライブラリのドキュメントを構築する方法
- [sync](http://nbdev.fast.ai/sync) によって Python モジュールから jupyter notebook にエクスポートする方法
- 並行して実行でき、ノートブックからCIにエクスポートできる[tests](http://nbdev.fast.ai/test)をノートブックに配置する方法
- [追加機能](http://nbdev.fast.ai/#Additional-functionality) に関する詳細情報を入手する

## インストール

nbdev は PyPI 上いあるため、次のように実行できます:
```
pip install nbdev
```

[編集可能なインストール](https://stackoverflow.com/questions/35064426/when-would-the-e-editable-option-be-useful-with-pip-install)のためには、以下のコマンドを使用します:
```
git clone https://github.com/fastai/nbdev
pip install -e nbdev
```

## 入門

独自のプロジェクトを開始するには:

- GitHub の場合は[ここ](https://github.com/fastai/nbdev_template/generate) をクリックしてください （このリンクが機能するためには、GitHub にログインする必要があります）。
- GitLab の場合は[ここ](https://gitlab.com/thomas.capelle/nbdev_template/generate) をクリックしてください。（このリンクが機能するためには、GitLab にログインする必要があります）。

要求された情報を入力し、*Create repository from template* をクリックすると、新しいGitHub または　GitLab リポジトリが作成されます。

**注意：** プロジェクトの名前は、nbdevによって生成されたPythonパッケージの名前になります。そのため、単語間に _ダッシュを付けずに_ 、すべて小文字の短い名前を選択することをお勧めします（アンダースコアは使用できます）。

次に、ターミナルを開き、作成したリポジトリを複製します。

または、cliコマンド `nbdev_new` を使用して、新しいnbdevプロジェクトを作成し、githubリポジトリを作成せずにgitリポジトリをローカルで初期化できます。

次に、`settings.ini` ファイルを編集します。
ライブラリをパッケージ化する準備が整ったときに必要なすべての情報が含まれているため、テンプレートによって提供される `setup.py`ファイルを変更する必要はありません。
基本的な構造（`settings.ini`で関連情報を変更すればパーソナライズできます）は、リポジトリのルートにノートブックが含まれることと、ドキュメントが自動生成されるフォルダ `docs` が含まれることです。
それは [jekyll](https://jekyllrb.com/) で動くWebサイトのためのすべてを含んでいます。
[GitHub PagesはJekyllをサポートしている](https://help.github.com/en/github/working-with-github-pages/setting-up-a-github-pages-site-with-jekyll)ため、追加の設定なしでGitHubでサイトを無料でホストできます。

`settings.ini` はnbdev の必須構成情報のすべての部分を探す場所です。
それを編集したら、コマンド `nbdev_build_lib` を実行します（`nbdev` のインストール時に自動的にインストールされます。
これで、 `settings.ini`で` lib_name`に設定した名前の新しいディレクトリが作成されました。

次に、 `jupyter notebook`を実行し、` 00_core.ipynb` をクリックします。
ここで、最初のモジュールを作成します。
他のノートブックと同じようにJupyterセルを作成します。
Pythonモジュールに含めるセルの場合、セルの最初の行として `#export` と入力します。
作成する新しい.ipynbの場合は、 `＃default_exp target_module_name`も入力する必要があります。これにより、生成されたモジュールの名前が定義されます（lib_name/target_module_name.py）。


ノートブックの最後のセルで、次を実行できます。

```
from nbdev.export import *
notebook2script()
```

    Converted 00_export.ipynb.
    Converted 01_sync.ipynb.
    Converted 02_showdoc.ipynb.
    Converted 03_export2html.ipynb.
    Converted 04_test.ipynb.
    Converted 05_merge.ipynb.
    Converted 06_cli.ipynb.
    Converted 07_clean.ipynb.
    Converted 99_search.ipynb.
    Converted index.ipynb.
    Converted tutorial.ipynb.


または、ライブラリを開発しているフォルダーのどこかにいる限り、コマンドラインで次のコマンドを実行できます:
``` bash
nbdev_build_lib
```

これらのどちらでも同じことが行われます。エクスポートしたすべてのセルをノートブックに含めるようにモジュールを更新します。

GitHubリポジトリでドキュメントを有効にするには、メインリポジトリページの'Settings'をクリックし、'GitHub Pages'までスクロールして、'Source'の下で 'master branch /docs folder' を選択します。
GitHubは作業中のドキュメントサイトへのリンクを表示します。

最後に、`index.ipynb`を編集します。
これはプロジェクトの *README* ファイルに変換され、ドキュメントのインデックスにもなります（現在読んでいるページは、実際には `index.ipynb` ファイルから取得されます！）
あなたはこのライブラリにエクスポートしたモジュールを使用できます。つまり、実際に機能するコードと実際の出力を表示できます。
必要なものがすべて揃ったら、ターミナルで `nbdev_build_docs` を実行します。
これにより、ノートブックのHTMLバージョンが `docs` ディレクトリにエクスポートされ、バッククォート内の単語（モジュールに存在する限り）のハイパーリンクが作成されます。
また、作成したすべてのノートブックのメニューと、それぞれの目次も作成します。

#### プロジェクトルートの代わりにサブディレクトリを使用して.ipynbファイルを含める場合

パラメータnbs_pathをプロジェクトルート以外に設定した場合、追加の手順なしに生成されたモジュールをインポートすることはできません。
- これらのモジュールをローカルにインストールします。これは、それらの相対インポートによりトップレベルのパッケージを超えてしまうためです。これは、プロジェクトルートで `pip install -e .` を実行して、編集可能なモードで環境にモジュールをインストールすることで実行できます。
- または、ノートブックフォルダーにライブラリフォルダーへのsimlinkを作成します。これは、 `ln -s lib_path lib_name`を実行することで実行できます（`lib_path`と `lib_name`をユースケースに合わせて調整します）。

## 追加機能

`nbdev` には多くの機能があります。 すべての機能については、サイドバーの各モジュールのドキュメントをご覧ください。 ここでは、couple を簡単に紹介します。

### プロジェクトをpypiに追加する

`pip install your-project` と入力するだけでプロジェクトをインストールできるようにするには、[pypi](https://pypi.org/) にアップロードする必要があります。
良いニュースは、あなたのプロジェクト用に完全にpypiに準拠したインストーラーがすでに作成されていることです！
そのため、行う必要があるのは、pypiに登録していない場合は、それを登録し、ログインの詳細を含む `~/.pypirc` というファイルを作成することだけです。 これらのコンテンツが必要です

```
[pypi]
username = your_pypi_username
password = your_pypi_password
```

もう1つ必要なのは `twine` なので、一度実行する必要があります。
```
pip install twine
```

プロジェクトをpypiにアップロードするには、プロジェクトのルートディレクトリに`make pypi`と入力するだけです。 完了すると、pypi上のプロジェクトへのリンクが出力されます。

*注意：** 新しいリリースをpypiにプッシュするたびに、`settings.py` のバージョン番号をインクリメントしてください。

### Gitの競合の回避と処理

Jupyter Notebookはgitの競合で問題を引き起こす可能性がありますが、 `nbdev`を使用すると作業がはるかに簡単になります。
最初のステップとして、プロジェクトフォルダーからターミナルで `nbdev_install_git_hooks`を実行します。
これにより、コミット時にノートブックからメタデータを削除するgitフックが設定され、競合が発生する可能性が大幅に減少します。

ただし、競合が発生した場合は、 `nbdev_fix_merge filename.ipynb` を実行してください。
これにより、セル出力の競合がバージョンに置き換えられます。入力セルに競合がある場合、両方のセルが標準の競合マーカー（`=====`など）とともにマージされたファイルに含まれます。
次に、Jupyterでノートブックを開き、保持するバージョンを選択できます。

### CIの一部としてnbdevを使用する

[GitHub actions](https://github.com/features/actions)を使用して、nbdevの機能を活用し、次のようなCIを簡単に作成できます:

- ノートブックが読み取り可能であることを確認します（`nbdev_read_nbs`を使用）
- （`nbdev_clean_nbs`を使用して）マージの競合を回避するために、ノートブックから不要なメタデータが削除されていることを確認してください
- ノートブックとエクスポートされたライブラリの間に差異がないことを確認します（`nbdev_diff_nbs`を使用）
- ノートブックでテストを実行します（`nbdev_test_nbs`を使用）

テンプレートには、上記の4つのポイントを使用する基本的なCIが含まれています。ファイル `.github/workflows/main.yml` を好みに合わせて編集し、不要な部分をコメント化します。

### 数学方程式のサポート

nbdevは方程式をサポートしています（優れた[KaTeX library](https://katex.org/)を使用しています）。 `_config.yml`の` use_math：true` で有効にします（デフォルトで有効になっています）。
以下の方法を使用して、ノートブックのドキュメントに数学を含めることができます。

`$$`を使用して、たとえば:

```
{% raw %}
$$\sum_{i=1}^{k+1}i$$
{% endraw %}
```

これは次のようにレンダリングされます:

> $$\sum_{i=1}^{k+1}i$$

`$`を使用して、たとえば:

```
このバージョンはインラインで表示されます: $\sum_{i=1}^{k+1}i$ 。 前後にテキストを含めることができます。
```

Which is rendered as:

> このバージョンはインラインで表示されます:$\sum_{i=1}^{k+1}i$ . 前後にテキストを含めることができます。

### カスタム検索エンジン

ドキュメントサイトに検索を追加するために、nbdevは[Google Custom Search](https://cse.google.com/cse/all)をサポートしています。これには、検索クエリを入力するときのオートコンプリートが含まれます。 このページの上部にある検索ボックスを使用して試してみることができます。

検索エンジンの作成を完全に自動化することはできませんが（Googleにログインして行う必要があるため）、これは非常に簡単になりました。
実行する必要がある手順は次のとおりです：[Setting up search](https://nbdev.fast.ai/search)。

## Contributing

`nbdev`に寄稿したい場合は、[contributions guidelines](https://github.com/fastai/nbdev/blob/master/CONTRIBUTING.md)を確認してください。
このプロジェクトは、fastaiの[code of conduct](https://github.com/fastai/nbdev/blob/master/CODE-OF-CONDUCT.md) に準拠しています。
参加することにより、あなたはこのコードを守ることが期待されます。
一般に、fastaiプロジェクトは、オープンソースソフトウェア開発で一般に受け入れられているベストプラクティスを遵守するよう努めています。

次のコマンドを実行して、使用するgitフックがインストールされていることを確認してください
```
nbdev_install_git_hooks
```
クローンされたリポジトリフォルダ内で。

## Copyright

Copyright 2019 onwards, fast.ai, Inc. Licensed under the Apache License, Version 2.0 (the "License"); you may not use this project's files except in compliance with the License. A copy of the License is provided in the LICENSE file in this repository.
