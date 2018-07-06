## Setting Amazon Polly for Wordpress

以前にも実験でAmazon PollyをWordpressに導入していました。

もう一度、入れてみようと思います。

<hr />




まず、IAM Policyを作成します。

JSONに以下をぶち込めば、とりあえずOKかな・・・。（乱暴）

<pre><code>{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "Permissions1",
            "Effect": "Allow",
            "Action": [
                "polly:SynthesizeSpeech",
                "s3:HeadBucket",
                "polly:DescribeVoices"
            ],
            "Resource": "*"
        },
        {
            "Sid": "Permissions2",
            "Effect": "Allow",
            "Action": [
                "s3:ListBucket",
                "s3:GetBucketAcl",
                "s3:GetBucketPolicy",
                "s3:PutObject",
                "s3:DeleteObject",
                "s3:CreateBucket",
                "s3:PutObjectAcl"
            ],
            "Resource": "arn:aws:s3:::audio_for_wordpress*"
        }
    ]
}</code></pre>

<ul>
<li><b>名前：</b>AmazonPollyWordpressPolicy</li>
<li><b>説明：</b>省略します。入れなくても良い。</li>
</ul>

次にIAM Userを作成します。

<ul>
<li><b>名前：</b>AmazonPollyWordpressUser</li>
<li><b>アクセスの種類：</b>プログラムによるアクセス</li>
<li><b>アクセス権限を設定：</b>既存のポリシーを直接アタッチ</li>
<li><b>ポリシータイプ：</b>AmazonPollyWordpressPolicy</li>
</ul>

これでAWS access key と AWS secret key が払い出されるので、Wordpress Plug-inに入力します。

細かな設定は自分でやってね。

Mizukiちゃんを選ぶとか、Tokyoリージョンを選ぶとか・・・。

投稿の上に出すのか下に出すのかも設定できます。
