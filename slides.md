---
theme: dracula
---

# 生成AIアプリのプロトタイピングサイクルを効率よく回す ClaudeCode活用術

2025/07/25 kansai.ts#11

---
layout: author
---

![icon](./images/icon.png)

## いずりょー / is_ryo

#PdM, EngineeringManager@Sprocket

#TypeScriptが好き #JavaScriptは嫌い

#kansai.ts Organizer

#フロントエンドカンファレンス関西実行委員

X → @is_ryo

---
layout: section
---

# 前提

---
---

# 弊社の生成AI事情

<div text-2xl>

- <div leading-relaxed>生成AIプロダクトを開発・リリースしている</div>

- <div leading-relaxed>生成AIを活用してどんな課題を解決してほしいのかユーザー側の解像度がまだまだ低い</div>

- <div leading-relaxed>どんな生成AIを活用したソリューションが求められているのかを把握するためにプロトタイピングが重要</div>
  
  - <div leading-relaxed>プロトタイプを作る→試す→評価するのサイクルをいかに早く回すか</div>

  - <div leading-relaxed>生成AIをうまく活用してサイクルを回す速度を上げたい</div>

- <div leading-relaxed>ClaudeCodeを使ってプロトタイピングをやる個人的Tipsを紹介していく</div>

  - <div leading-relaxed>プロトタイピングに限らず普段の開発でも一定役立つかも…</div>

</div>

---
layout: center
---

<div font-bold text-5xl leading-relaxed>今日は私自身の経験談からお話します。<br />※すべて個人の意見です。</div>

---
layout: section
---

# 今日伝えたいこと

---
layout: section
---

# 生成AIに<strong>何を伝えるか</strong>が9割

---
---

# 生成AIに<strong>何を伝えるか</strong>が9割

<div text-2xl>

- <div leading-relaxed>生成AIに持たせるコンテキストはどんな情報でどんな粒度なのかで、アウトプットの質が9割決まると思っている</div>

  - <div leading-relaxed>プロンプトエンジニアリングじゃなくてコンテキストエンジニアリングという概念が流行っているらしい</div>

- <div leading-relaxed>作業する中で都度知っておいてほしいコンテキストもあるし、特定の作業のときだけでいいコンテキストもある</div>

- <div leading-relaxed>ClaudeCodeはこういったコンテキストの渡し方についてもHackableなので、色々工夫できる</div>

- <div leading-relaxed>今日はその中で最近個人的流行りのTipsを紹介します</div>

</div>

---
---

# 本日紹介するTips

<div text-4xl>

1. CLAUDE.mdを整備する

2. ガードレールを引く

3. kiro的アプローチ

4. サンプルコードを用意する

</div>

---
---

# CLAUDE.mdを整備する

<div text-2xl>

- <div leading-relaxed>ClaudeCodeを使ったことがある人ならみんなやってるだろうけど、これが結構重要だったりする</div>

- <div leading-relaxed><code>/init</code>ですでにあるコードを読み込んである程度の仕様書だったり、ルールを作成してくれる</div>

- <div leading-relaxed>作成してくれたCLAUDE.mdを確認して、細かいところを調整している</div>

  - <div leading-relaxed>「(このあと詳細を説明しますが)作業するときはこのドキュメントを理解してから作業に入る」とか</div>

  - <div leading-relaxed>「こういう場合はユーザーに確認すること」とか</div>

  - <div leading-relaxed><code>#</code>をつけてclaudeに指示するとCLAUDE.mdに追記してくれる</div>

</div>

---
---

# ガードレールを引く


<div text-2xl>

- <div leading-relaxed>ガードレール = 約束事・制約を用意してClaudeCodeが生成するコードの品質を一定担保する</div>

- <div leading-relaxed>コーディング規約やスタイルガイド、設計思想などをMarkdownに書いておき、これらを理解させて作業させる</div>

  - <div leading-relaxed>「エラーハンドリングの記述例をTSで書いておく」とか「SOLID原則にしたがった構成にしなさい」とかスコープは様々</div>

- <div leading-relaxed>「<strong>book</strong>」という概念でClaudeCodeに読み込ませている</div>

  - <div leading-relaxed>bookというディレクトリを用意して、index.mdに目次を書いておき、ClaudeCodeはこの目次から必要な情報を取得してコンテキストとして理解することができる</div>

</div>

---
---

# kiro的アプローチ


<div text-2xl>

- <div leading-relaxed>最近AWSから出たIDE「Kiro」のアプローチを真似たcommandを作って、設計やタスク分解をさせてから作業をさせている</div>

  - <div leading-relaxed><code>./.claude/commands/{command_name}</code>以下にMarkdownなどを配置しておくと<code>/command_name hogehoge</code>という形でカスタムコマンドを用意できる</div>

- <div leading-relaxed>Kiroは<strong>設計力</strong>に強みを持っているので、その強みをcommandとして移植した</div>

- <div leading-relaxed><code>/kiro チャットUIを実装して</code>と依頼すると、要件定義→設計→タスク分解をユーザーに確認を求めながらドキュメントを作成し、作業を実行するようにできる</div>

  - <div leading-relaxed>今のところこのやり方をしていると行ってほしい方向に実装をしてくれる確率がグッと上がっている</div>

</div>

---
---

# サンプルコードを用意する


<div text-2xl>

- <div leading-relaxed>まだ新しいパッケージの利用方法とか、個別で作っているMCPサーバーへのアクセス方法などについてはサンプルコードを用意して、それを生成AIに伝えるようにしています</div>

- <div leading-relaxed>こうすることで古い情報や誤った情報に振り回されて失敗を繰り返すことを回避できる</div>

- <div leading-relaxed>そこまでしっかり書かなくても良くて、ある程度省略した書き方をしていてもうまくいくケースが多い</div>

</div>

---
layout: center
---

<div font-bold text-5xl leading-relaxed>簡単にデモします</div>

---
---

# まとめ

<div text-2xl>

- <div leading-relaxed>生成AIは便利だけど<strong>よしなにアウトプットを出すことはできない</strong>ので、コンテキストを整備したり、何を作って欲しいのかを理解させたりするのが重要</div>

  - <div leading-relaxed>コンテキストの中には「仕様」「ルール」「思想」など様々な情報があり、それらを生成AIが理解しやすい形で用意しておく</div>

  - <div leading-relaxed>アウトプットがブレないように要件定義書→設計書→タスク詳細を用意してから作業させると、かなり精度がいいアウトプットを出すことができる</div>

- <div leading-relaxed>ClaudeCodeはHackableな設計なのでエンジニアリングに適した改造ができるので最大限活用しよう</div>

  - <div leading-relaxed>commandで作業のショートカットを用意したり、hookで自動でLintを実行させたり</div>

</div>

---
layout: center
---

<div font-bold text-5xl leading-relaxed>Thanks!!!</div>
