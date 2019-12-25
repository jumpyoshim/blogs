GitHub の Contributions calendar、通称「芝生」に GitLab のコントリビュートを反映させる方法をご紹介します。

この記事は `今年イチ！お勧めしたいテクニック by ゆめみ feat.やめ太郎 Advent Calendar 2019` の 24 日目の記事です。

# 芝生って何？

正式名称は [Contributions calendar](https://help.github.com/en/articles/viewing-contributions-on-your-profile) で、コントリビュートアクティビティを可視化してくれる機能です。

![contributions_graph.png](https://qiita-image-store.s3.amazonaws.com/0/160547/c949b133-7e94-1f5a-5ca4-c4c2bcb94668.png)

出典： [GitHub Help](https://help.github.com/en/articles/viewing-contributions-on-your-profile#contributions-calendar)

その見た目から日本では通称「芝生」と呼ばれ、コントリビュートすることを「草を生やす」と言われるようになりました。

参考：[GitHub 芝生入門/芝生応用](https://qiita.com/sta/items/2c1f0252a6a9ce5e2087)

# なぜ草を生やすのか

エンジニアであれば

**「草生やして転職。」**

という文言を Twitter で見たことがある方は多いと思います。

<blockquote class="twitter-tweet" data-lang="ja"><p lang="ja" dir="ltr">「草生やして転職。」<br><a href="https://twitter.com/hashtag/GitHub?src=hash&amp;ref_src=twsrc%5Etfw">#GitHub</a> 連携するだけで、スキル審査開始。<br>スキル偏差値60以上の <a href="https://twitter.com/hashtag/%E3%82%A8%E3%83%B3%E3%82%B8%E3%83%8B%E3%82%A2?src=hash&amp;ref_src=twsrc%5Etfw">#エンジニア</a> 限定で、Tech企業トップ100+からオファーが届く   <br> <a href="https://t.co/BgX4PXYehR">https://t.co/BgX4PXYehR</a></p>&mdash; ハイスキルなエンジニアの転職 Findy (@findy_code) <a href="https://twitter.com/findy_code/status/894952627611422721?ref_src=twsrc%5Etfw">2017年8月8日</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

これは [Findy](https://findy-code.io) という転職サービスの文言なのですが、GitHub のアクティビティを偏差値化して企業とエンジニアをマッチングさせるという面白いサービスです。

![findy-skill-image.png](https://qiita-image-store.s3.amazonaws.com/0/160547/a993c810-54bb-28ff-abf4-11598d3c95d8.png)

出典：[Findy「スキル偏差値」のアルゴリズム更新および 80 段階へのアップデートのお知らせ](https://findy-code.io/engineer-lab/skill-deviation-value-update20171016)

また、Findy に似たようなサービスで [Forkwell](https://forkwell.com/) というものもあり、GitHub のアクティビティから言語ごとにスキルレベルという形で数値化をしていたり、曜日ごと時間ごとのアクティビティを可視化していたりしてこちらも面白いサービスです。

![img_5c2ec5ee15368.png](https://qiita-image-store.s3.amazonaws.com/0/160547/7e9e71dd-f4d4-68a4-d400-6b8444783790.png)

出典：[Forkwell サービス 全 6 種類を最大限活用する使い方のコツ](https://forkwell-navi.com/forkwell-%E3%82%B5%E3%83%BC%E3%83%93%E3%82%B9/)

また、2018 年 8 月に正式リリースされた [LAPRAS](https://lapras.com/)は、GitHub だけでなく SNS や connpass、そして Qiita のアクティビティから個人のスキルを可視化してくれるサービスです。

![top-1024x676.jpg](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/160547/fa367b8f-7dd4-7274-232d-2995c94d47f2.jpeg)

出典：[履歴書なし、応募なしで自分が転職できそうな企業がわかる！興味通知機能をリリース](https://corp.lapras.com/news/254/)

これらのサービスは GitHub のアクティビティなどからエンジニアのスキルを数値化・可視化してくれるので、転職サービスとしてではなく自己分析として使うのもアリですし、自己研鑽のモチベーションを上げるために使うのもアリだと思います。

自分の頑張りが可視化されるのは嬉しいですよね。

# GitLab にも芝生がある

GitLab の場合は<font color="Blue">青色</font>なので芝生と言っていいのかわからないですが、実は同じようにコントリビュートアクティビティを可視化してくれる機能があります。

<img width="757" alt="Screen Shot 2019-03-08 at 18.08.19.png" src="https://qiita-image-store.s3.amazonaws.com/0/160547/32368537-30ac-b116-b56d-1a2884326937.png">

GitHub と同じように GitLab のアクティビティも可視化したいですよね。

しかし残念ながら、現時点（2019 年 12 月）では Findy や Forkwell は GitLab に対応していません...😢

ですが、救いの道はあります。

# GitLab に草生やしたら GitHub にも草生やす

だいぶ長々と書いてきましたがようやく本題です。

GitLab のコントリビュートアクティビティを GitHub にも反映させるために、GitLab の [Repository mirroring](https://docs.gitlab.com/ce/workflow/repository_mirroring.html) という機能を利用します。

GitLab にソースコードがプッシュされたら自動的に GitHub にもプッシュしてくれるという便利な機能です。

設定方法はとても簡単で、以下の 4 ステップです。

> 1. Create a [GitHub personal access token](https://help.github.com/en/articles/creating-a-personal-access-token-for-the-command-line) with the `public_repo` box checked.

2. Fill in the Git repository URL field using this format: `https://\<your_github_username>@github.com/\<your_github_group>/\<your_github_project>.git.`
3. Fill in Password field with your GitHub personal access token.
4. Click the Mirror repository button.

参考: [Setting up a push mirror from GitLab to GitHub](https://docs.gitlab.com/ce/workflow/repository_mirroring.html#setting-up-a-push-mirror-from-gitlab-to-github-core)

「最初から GitHub で開発すればいいじゃん！」という反応ももちろんあると思っているのですが、GitLab もなかなかいいものですよ 😉

参考：[Gitlab に触ってみて、Github と比較した](https://qiita.com/developer-kikikaikai/items/3fd1277a9a5778000638)

手前味噌で恐縮ですが自分が以前書いた記事も紹介させていただきます。

参考：[知って「おっ！」てなった GitLab の知識 7 選](https://qiita.com/jumpyoshim/items/d5a63bdd3681843866f8)

# おわりに

隣の芝生が青く見えた方はぜひ GitLab も使ってみてください。

（これが言いたかっただけ感は否めません。最後までお付き合いいただきありがとうございました！）
