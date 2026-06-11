LINE LIFF用 事前問診フォーム
接骨院のLINE LIFFエンドポイントURLに登録する想定の、静的HTMLだけで動く簡易版の事前問診フォームです。
ファイル構成
index.html: フォーム本体です。CSSとJavaScriptもこの1ファイルに含めています。
README.md: 公開手順と設定方法です。
AGENTS.md: このプロジェクトを編集するときの開発ルールです。
GitHub Pagesで公開する手順
このフォルダの内容をGitHubリポジトリにpushします。
GitHubのリポジトリ画面で Settings を開きます。
左メニューの Pages を開きます。
Build and deployment の Source で Deploy from a branch を選択します。
Branch で公開したいブランチを選び、フォルダは / (root) を選択して保存します。
数分後に表示される https://ユーザー名.github.io/リポジトリ名/ が公開URLです。
ブラウザで公開URLを開き、フォームが表示されることを確認します。
index.html がリポジトリ直下にある場合、GitHub Pagesの公開URLを開くとそのままフォームが表示されます。
GAS_ENDPOINTの差し替え手順
index.html 内の次の行を探してください。
const GAS_ENDPOINT = "https://script.google.com/macros/s/AKfycbxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx/exec";
Google Apps ScriptをWebアプリとしてデプロイしたあと、発行されたWebアプリURLに差し替えます。
const GAS_ENDPOINT = "https://script.google.com/macros/s/実際のデプロイID/exec";
フォーム送信時は、fetch で GAS_ENDPOINT にJSON形式のPOSTを送ります。GAS側ではPOSTされたJSONを受け取り、スプレッドシートに保存する処理を実装してください。
LIFF登録時のエンドポイントURL
LINE DevelopersコンソールでLIFFアプリを作成し、エンドポイントURLにGitHub Pagesの公開URLを設定します。
例:
https://ユーザー名.github.io/リポジトリ名/
このHTMLにはまだLINE LIFF SDKを読み込んでいません。あとでLINEログイン情報やプロフィール情報を使う場合は、index.html のコメント箇所にLIFF SDKの読み込み、liff.init()、プロフィール取得処理を追加してください。
入力項目
氏名
フリガナ
電話番号
ご来院状況
本日気になる部位
部位ごとの詳細
あなたが感じる痛みレベル
いつから
きっかけ
電気治療を受けて具合が悪くなったことはありますか？
本日伝えたいこと
必須項目が未入力のまま送信された場合は、画面上にエラーを表示します。
手の指 と 足の指 を選択した場合は5本の各指を選択でき、それ以外の具体的な部位を選択した場合は 左 / 右 を選択できます。部位詳細は bodyPartDetails としてJSONに含まれます。
いつから はカレンダー式の日付入力です。きっかけ は任意入力、電気治療に関する確認は必須の選択式です。
