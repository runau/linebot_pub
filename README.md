# lineBot
awsとpythonの勉強と、自分の癒しと、節約と、スケジュールとTODOを忘れないために趣味で作っているもの。
だったのですが、商品化につき、プライベートリポジトリに移行しました…。
こちらとりあえず作った業者ページ！

[エンジョイクリエイト](https://encr.jp)

話す人話す人にダサいって言われるけど…
知ってる。知ってるけど、これが私の限界ww
諦めて開き直る！

とにかく楽しく作るの！で、お金が付いてきたら最高だよね？
しかもね、エンジョイクリエイトって会社ないのよ？
かぶらないのよ？
検索したら一番上なのよ？
いいじゃないか……


## ぶるーでぃちぇっかー
対企業に物を売るために、とりあえず実績を作るべく開発したもの。
生理予定日と排卵予定日がボタンタップだけで予測できます。
通知もされます。
[ぶるーでぃちぇっかー](https://encr.jp/blue)


## ゆいちゃん
開発環境として使っているから、すぐ調子悪くなるけど、
よかったら遊んであげて下さい！
一応ちゃんと動くようになるのは6末を目指しています！
[ゆいちゃん](https://lin.ee/kap69GX)


## 使ってるもの(一部これから作りたい＆使いたいもの)
pegmatiteという神様ツールをclomeにアドインすると、↓のumlが全部図で見れます！
https://chrome.google.com/webstore/detail/pegmatite/jegkfbnfbfnohncpcfcimepibmhlkldo

### プログラム本体
こんな感じで動いている。
設定ファイルがdynamoに入ってて、ゆいちゃんも予約アプリもぶるーでぃちぇっかーも同じプログラムで出来てる。
awsじゃないものはどうやって書いたらいいんだろう…
独自画像埋め込みたいんだけど…。
```uml
@startuml
!define AWSPUML https://raw.githubusercontent.com/milo-minderbinder/AWS-PlantUML/release/18-2-22/dist
!includeurl AWSPUML/common.puml
!includeurl AWSPUML/ApplicationServices/AmazonAPIGateway/AmazonAPIGateway.puml
!includeurl AWSPUML/Compute/AWSLambda/AWSLambda.puml
!includeurl AWSPUML/Database/AmazonDynamoDB/AmazonDynamoDB.puml
!includeurl AWSPUML/General/AWScloud/AWScloud.puml
!includeurl AWSPUML/General/client/client.puml
!includeurl AWSPUML/General/mobileclient/mobileclient.puml
!includeurl AWSPUML/General/user/user.puml
!includeurl AWSPUML/Storage/AmazonS3/AmazonS3.puml
!includeurl AWSPUML/Storage/AmazonS3/bucket/bucket.puml
!includeurl AWSPUML/General/traditionalserver/traditionalserver.puml
skinparam componentArrowColor Black
skinparam componentBackgroundColor White
skinparam nodeBackgroundColor White
skinparam agentBackgroundColor White
skinparam artifactBackgroundColor White

USER(user)
MOBILECLIENT(line)
TRADITIONALSERVER(messagingApi,messagingApi)
AWSCLOUD(aws) {
 AMAZONS3(s3) 
 AMAZONAPIGATEWAY(api)
 AWSLAMBDA(lambda) 
 AMAZONDYNAMODB(dynamo) 
}
user -d-> line
line -d-> messagingApi
messagingApi -d-> api
api -d-> lambda
lambda -d-> s3
api <-d- lambda
messagingApi <-d- api
line <-d- messagingApi
user <-d- line

s3 -d-> line
lambda -d-> s3
lambda -d-> dynamo
dynamo -d-> lambda
@enduml
```

### CI/CD
```uml
@startuml
!define AWSPUML https://raw.githubusercontent.com/milo-minderbinder/AWS-PlantUML/release/18-2-22/dist
!includeurl AWSPUML/common.puml
!includeurl AWSPUML/ApplicationServices/AmazonAPIGateway/AmazonAPIGateway.puml
!includeurl AWSPUML/Compute/AWSLambda/AWSLambda.puml
!includeurl AWSPUML/General/AWScloud/AWScloud.puml
!includeurl AWSPUML/General/user/user.puml
!includeurl AWSPUML/Storage/AmazonS3/AmazonS3.puml
!includeurl AWSPUML/ManagementTools/AWSCloudFormation/AWSCloudFormation.puml
!includeurl AWSPUML/DeveloperTools/AWSCodePipeline/AWSCodePipeline.puml
skinparam componentArrowColor Black
skinparam componentBackgroundColor White
skinparam nodeBackgroundColor White
skinparam agentBackgroundColor White
skinparam artifactBackgroundColor White

USER(user)
AWSCLOUD(aws) {
  AWSCODEPIPELINE(pipeline)
  AWSCLOUDFORMATION(cloudFormation) 
  AMAZONS3(s3) 
  package dev {
    AMAZONAPIGATEWAY(api_dev)
    AWSLAMBDA(lambda_dev) 
  }
  package prod {
    AMAZONAPIGATEWAY(api)
    AWSLAMBDA(lambda) 
  }
}

user -d-> pipeline
pipeline -d-> cloudFormation
cloudFormation -d-> s3
cloudFormation <-d- s3
cloudFormation -d-> lambda
cloudFormation -d-> api
cloudFormation -d-> lambda_dev
cloudFormation -d-> api_dev

@enduml
```


## もうちょい細かい自分のメモ

```uml
@startuml
!define AWSPUML https://raw.githubusercontent.com/milo-minderbinder/AWS-PlantUML/release/18-2-22/dist
!includeurl AWSPUML/common.puml
!includeurl AWSPUML/ApplicationServices/AmazonAPIGateway/AmazonAPIGateway.puml
!includeurl AWSPUML/Compute/AWSLambda/AWSLambda.puml
!includeurl AWSPUML/Compute/AWSLambda/LambdaFunction/LambdaFunction.puml
!includeurl AWSPUML/Database/AmazonDynamoDB/AmazonDynamoDB.puml
!includeurl AWSPUML/Database/AmazonDynamoDB/table/table.puml
!includeurl AWSPUML/General/AWScloud/AWScloud.puml
!includeurl AWSPUML/General/client/client.puml
!includeurl AWSPUML/General/mobileclient/mobileclient.puml
!includeurl AWSPUML/General/user/user.puml
!includeurl AWSPUML/Storage/AmazonS3/AmazonS3.puml
!includeurl AWSPUML/Storage/AmazonS3/bucket/bucket.puml
!includeurl AWSPUML/General/traditionalserver/traditionalserver.puml
skinparam componentArrowColor Black
skinparam componentBackgroundColor White
skinparam nodeBackgroundColor White
skinparam agentBackgroundColor White
skinparam artifactBackgroundColor White

USER(user)
MOBILECLIENT(line)
TRADITIONALSERVER(messagingApi)
AWSCLOUD(aws) {
 AMAZONS3(s3) {
  BUCKET(temporary,temporary)
  BUCKET(public,public)
 }
 AMAZONAPIGATEWAY(api)
 AWSLAMBDA(lambda) {
  LAMBDAFUNCTION(linebotWebhook,linebotWebhook)
  LAMBDAFUNCTION(analysis,analysis)
  LAMBDAFUNCTION(getReplyMessage,getReplyMessage)
  LAMBDAFUNCTION(getLineBotUserData,getLineBotUserData)
  LAMBDAFUNCTION(editLineBotDynamo,editLineBotUserData)
  LAMBDAFUNCTION(putLineBotDynamo,putLineBotUserData)
  LAMBDAFUNCTION(putLineBot,putLineBotMaster)
 }
 AMAZONDYNAMODB(dynamo) {
   TABLE(master,master)
   TABLE(trn,trn)
 }
}
user -d-> line
line -d-> messagingApi
messagingApi -d-> api
api -d-> linebotWebhook
api <-d- linebotWebhook
messagingApi <-d- api
line <-d- messagingApi
user <-d- line

linebotWebhook -d-> analysis
linebotWebhook -d-> getReplyMessage
linebotWebhook <-d- analysis
linebotWebhook <-d- getReplyMessage
getReplyMessage -d-> editLineBotUserData
getReplyMessage -d-> putLineBotUserData
getReplyMessage -d-> getLineBotUserData
getLineBotUserData -d-> temporary
temporary -d-> line
public -d-> line
putLineBotUserData -d-> trn
getLineBotUserData -d-> trn
editLineBotUserData -d-> trn
getReplyMessage -d-> putLineBot
putLineBot -d-> master
@enduml
```


