# AI Nights **ボーナス** コンテンツ - Beginner Track

## マシンの前提条件

* デモに必要な画像とコードサンプルを入手するために、このリポジトリをあなたのローカルマシンにクローンしてください。

  ```:bash
  git clone https://github.com/amynic/ainights-sessionowners.git
  ```

* [Microsoft Azure Subscription](https://azure.microsoft.com/ja-jp/free/) をご用意下さい。
* モダンなブラウザー (Google Chrome, Microsoft Edge) がインストールされていること。
* [Postman](https://www.getpostman.com/downloads/) がインストールされていること。
  * Postman は API Development Environment です。Windows, Linux や macOS で利用可能です。
* docker がインストールされていること。
  * [Docker Desktop for Windows](https://docs.docker.com/docker-for-windows/)
  * [Docker Desktop for Mac](https://docs.docker.com/docker-for-mac/)
  * [Docker Engine - Community](https://docs.docker.com/install/)

> *すべてのデモやコンテンツは Windows でテストしていますが、MacOS や Linux で動作するようオプションを設定しています。もし他のオペレーティングシステムでのフィードバックがありましたら、issue やプルリクエストを通じて情報を提供いただけますと幸いです。*

## セクション一覧:

* **Task A:** Microsoft Azure Cognitive Services - Computer Vision [セクションへ](#task-a-microsoft-azure-cognitive-services---computer-vision)
* **Task B:** Microsoft Azure Cognitive Services - Text Analytics in a Container [セクションへ](#task-b-microsoft-azure-cognitive-services---text-analytics-in-a-container)
* **Task C:** Microsoft PowerApps [セクションへ](#task-c-microsoft-power-apps)

## Task A: Microsoft Azure Cognitive Services - Computer Vision

このタスクでは、ウェブサイトのデモオプションを使って Cognitive Services を試します。

このページを開きます: [https://azure.microsoft.com/ja-jp/services/cognitive-services/directory/vision/](https://azure.microsoft.com/ja-jp/services/cognitive-services/directory/vision/)

![Computer Vision website Link highlighted](/docs-images/computer-vision-link.png)

ここには、それぞれのセクションを試すためのたくさんのデモがあります。（画像内のシーンとアクティビティの認識、OCR、顔検出、表情検出、Video indexer など）

**Computer Vision** の下の **画像内のシーンおよびアクティビティ認識** のとなりの **デモ** というリンクをクリックします。（また、ここには様々なサービスを知るための他のデモのリンクもあります。）

![Computer Vision Example](/docs-images/computer-vision-demo.png)

ここでは、指定された画像にどのような情報があるかを検出するデモを体験できます。上図に示す画面の左側には対象の画像が表示され、検出されたオブジェクトが矩形で示されていることがわかります。また右側には検出されたデータが表示されています。

それでは、 **参照** ボタンをクリックし、 `sample-images/computer-vision-web-browser` ディレクトリの **cat.jpeg** または **city.jpeg** をアップロードします。

例えば **cat.jpeg** をアップロードすると、下図のように猫がオブジェクトとして検出されていることがわかります。また右の欄の情報から、猫が検出された旨を読み取ることができます。

![Computer Vision Cat Example](/docs-images/cat-sample.png)

## Task 2: Microsoft Azure Cognitive Services - Text Analytics via REST

つぎに、これらのサービスをアプリケーションに組み込むことを想定して、 REST プロトコルを用いて体験してみましょう。

まず、[Microsoft Azure](https://azure.microsoft.com/ja-jp/) にサインインし、右角にある **ポータル** をクリックして開きます。

次に、ポータルの左上にある **リソースの作成** をクリックし、検索欄で **Cognitive Services** を入力し候補から **Cognitive Services** を選択します。それから、Cognitive Services ブレードの **作成** をクリックします。

![Select Cognitive Services](/docs-images/cognitive-azure-001.png)
![Create Cognitive Services Account](/docs-images/cognitive-azure-002.png)

Cognitive Services のアカウントを作成するために詳細を入力します:

* **名前:** サービス名を入力する（例: ainightscognitive ）
* **サブスクリプション:** 利用するサブスクリプションを選択する
* **場所:** 最寄りの利用可能なデータセンターの場所を選択する（例: (アジア太平洋) 東日本）
* **価格レベル:** S0
* **リソースグループ:** '新規作成'をクリックし、リソースグループの名前を入力する（例: ainights ）
* **規約を読み、「以下の通知を読み、理解しました。」のチェックボックスにチェックする**
* **'作成' をクリックする**

![Cognitive Services Details](/docs-images/cognitive-details.png)

作成が完了したら、通知（画面右上）を開き、 **リソースに移動** をクリックします。

![Go to Resource](/docs-images/go-to-resource.png)

Cognitive Services のページで、 **キー**　をクリックし、 **キー 1** をコピーします。

![Copy Key](/docs-images/keys.png)

つぎに、左ペインから **概要** を開き、エンドポイントの値をコピーします。

![Copy Endpoint](/docs-images/endpoint.png)

Postman をダウンロードしインストールし、ローカルマシンに API の作業環境を整えます。

> Postman についてはこちら [マシンの前提条件 セクション](#マシンの前提条件) に掲載したリンクから、ダウンロードしてください。

Postman を開き、図中のウィンドウが表示されている場合は「Create New」タブの **Request** を選択します。ウィンドウが表示されていない場合は、左上の「New」をクリックすると表示されます。

![Create A Request](/docs-images/create-request.JPG)

下図のようにリクエストの詳細を入力し、 **+ Create Collection** をクリックし "Text Analytics Samples" と名前を入力します。

![Enter Request Details](/docs-images/save-request.JPG)

作成した collection を選択し、 **Save to Text Analytics Samples** をクリックして保存します。

![Save Request](/docs-images/save.JPG)

つぎに、 Text analytics API を呼び出すリクエストを作成します:

* 左上の GET リクエストを POST リクエストに変更する
* URL入力欄に、前述でコピーしたエンドポイントの URL を入力し、続いて `text/analytics/v2.0/sentiment` を入力する
* URL入力欄の下の Headers タブを開く
* キーに `Ocp-Apim-Subscription-Key` を入力し、値に前述でコピーした **KEY1** を入力する
* キーに `Content-Type` を入力し、値に `application/json` を入力する

* ![Headers and URL](/docs-images/url-and-headers.JPG)

* URL入力欄の下の Body タブを開く
* `raw` のラジオボタンを選択する
* `sample-code/cognitive-services-api-task/sentiment-analysis-text.json` の JSON をコピーし Body 入力欄にペーストする
* `Send` ボタンをクリックし、レスポンスを確認する。ポジティブな文は `score` が高く、ネガティブな要素が含まれている文は `score` が低く判定されていることがわかります。

* ![Body and Submit REST Request](/docs-images/rest-body.JPG)

また、REST API からほかのオプションを試すこともできます。例えば、 KeyPhrases 機能です。 URL の末尾を `sentiment` から `keyPhrases` に変更し、 `Send` をクリックしてキーフレーズの結果を確認しましょう。

* ![Key Phrases REST Request](/docs-images/keyphrases.JPG)

> Text Analytics API の言語のサポートについては、[こちら](https://docs.microsoft.com/en-gb/azure/cognitive-services/text-analytics/language-support/)からご参照ください。もしお使いの言語がサポートされていれば、JSON ファイルを編集してテキストを翻訳し、APIの動作を確認してみて下さい。例として、フランス語の JSON ファイルが `sample-code/text-analytics-demo/sentiment-analysis-text-fr.json` です。適宜変更してください。

> もし Postman を利用するにあたり問題があれば、 [sentiment analysis](https://northeurope.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c9/) や [key phrase extraction](https://northeurope.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c6/) の API ドキュメントからいつでも REST API のリクエストを発行することができます。利用しているデータセンターを選択し、Postman で利用したキーや body のサンプルを入力してご利用ください。

## Task B: Microsoft Azure Cognitive Services - Text Analytics in a Container

このデモはこの Azure ドキュメントに基づいたものです: [Install and run Text Analytics containers](https://docs.microsoft.com/en-us/azure/cognitive-services/text-analytics/how-tos/text-analytics-how-to-install-containers/)

このデモを実行するために、お手元のマシンに Docker をインストールする必要があります。

* [Download docker for your local machine here - available on Windows, Linux and macOS](https://docs.docker.com/docker-for-windows/)

Docker のインストーラーを実行し、ダウンロードが開始されたら、このように実行状況を確認することができます。

![Docker Download](docs-images/docker-download.JPG)

インストールされたら、 Docker を起動してください。（Windows の場合は、スタートメニューで `docker` と入力し、 Docker Desktop を選択します。）Docker デーモンが起動しているか確認してください。

Windows の場合は、タスクバーの通知領域（日付と時間の表示の近く）に Docker のアイコンが表示されていれば起動できています。

![Docker Running](docs-images/docker-running.JPG)

Cognitive Services Text Analytics API をローカルで実行するために、Docker イメージを取得する必要があります。コマンドプロンプトを開き、任意のディレクトリの配下で下記コマンドを実行してください。（もし適したディレクトリがなければ、 `AI-Nights` というディレクトリを作成するとよいでしょう。）

```
docker pull mcr.microsoft.com/azure-cognitive-services/sentiment:latest
```

すると、ローカルのレジストリに対して、Docker イメージのダウンロードが開始されます。

![Docker Pull success](docs-images/docker-pull-request-success.JPG)

> もし下図のようなエラーが発生する場合、 `docker` コマンドを実行する前に Docker デーモンが起動しているかをよく確認してください。確認するには [Getting Started Guide from Docker Here](https://docs.docker.com/docker-for-windows/) をお試しください。
![Docker Error](docs-images/possible-error.JPG)

ダウンロードが終わったら、指定した文章の感情スコアを得るためにコンテナを実行する準備をしましょう。

コンテナを起動するためには、前章で利用した **Cognitive Services エンドポイント** と **API キー** が必要になります。

> このコンテナがローカルで動いていることを確認したい場合は、インターネットの接続を切断してお試しください。

`docker run` コマンドは、下記（または、 [このファイル](sample-code/cognitive-containers/run-container-command.txt) ）のようになります。データセンターと API キーの値は適宜置換え、実行してください。

```
docker run --rm -it -p 5000:5000 --memory 4g --cpus 1 mcr.microsoft.com/azure-cognitive-services/sentiment Eula=accept Billing=https://<datacenter-here>.api.cognitive.microsoft.com/text/analytics/v2.0 ApiKey=<key>
```

このコンテナはあなたのローカルマシンで実行されています。

クエリの詳細を把握するには、この OpenAPI（旧 Swagger）の定義を確認してください: [http://localhost:5000/swagger/index.html](http://localhost:5000/swagger/index.html)

![Swagger Definition](docs-images/swagger.JPG)

API をテストするには、Postman で新しいリクエストを作成します:

* POST
* URL: http://localhost:5000/text/analytics/v2.0/sentiment
* Headers:
  * Content-Type : application/json
  * ![Postman Request for Containers](docs-images/container-postman.JPG)

* Body:
  * [前章](sample-code/text-analytics-demo/sentiment-analysis-text.json)のサンプル JSON を入力します
  * ![Postman Request for Containers Result](docs-images/container-result.JPG)

コンテナを停止するには、コマンドラインに戻り **CTRL + C** を入力してください。このようにアプリケーションが終了したことが確認できます。

![Application Shutdown](docs-images/application-shutdown.JPG)

## Task C: Microsoft Power Apps

### Creating a front end application to take a picture of a dog and analyse it

> NOTE: you must use your organizational account to use PowerApps. As this may become an issue 

Navigate to: [https://powerapps.microsoft.com/en-us/?WT.mc_id=build2019-event-amynic](https://powerapps.microsoft.com/en-us/) and sign in with your organizational account.

This will take you to the PowerApps main menu screen. Select the **Canvas App from Blank** button

![PowerApps main menu](docs-images/powerapps-main-menu.JPG)

Provide an App Name, **example: Dog Spotter** and in this case select **Format:Phone**

![PowerApps Create Canvas App](docs-images/powerapps-create-canvas-app.JPG)

This will load a screen like shown below. With a user interface for you to start building your application using the click-and-drag interface.

![PowerApps Blank App](docs-images/powerapps-blank-app.JPG)

To start building our app we are going to need to insert some functionality. You will find the **insert** menu at the top of the page like below

![PowerApps Insert Tab](docs-images/powerapps-insert-tab.JPG)

First we are going to insert **Camera** functionality. Under the insert tab select the **Media** dropdown and select the **Camera** option

![PowerApps Insert Camera](docs-images/powerapps-insert-camera.JPG)

Position the camera in good place on the page and you will see a properties pane appear on the right side of the page

Choose the **Advanced** tab from the properties pane. Under **Action** and **OnSelect** insert

``` Collect(myPics, Camera1.Photo) ```

![PowerApps Camera Logic](docs-images/powerapps-camera-logic.JPG)

Next we are going to insert a title for the application. Go to the **insert** tab and select the **Text** dropdown menu. Under this menu select **Label**

![PowerApps Insert Title](docs-images/powerapps-insert-title.JPG)

Place the Title at the top of the page. Under the properties pane on the right update the options below:
* **Text:** Dog Spotter (or another application name you would like)
* **Font Size:** 60
* **Text Alignment:** Center

> Making other changes on the properties pane will change the look and information within your app. Please investigate the options available to you. In this tutorial we will only look at a few

![PowerApps Title Information](docs-images/powerapps-title-info.JPG)

Now we are going to insert a **Photo Gallery**. When a photo is taken it will appear in the app at the bottom of the page.

Go to the **Insert** tab and select **Gallery**. Choose the **Horizontal** option and position the item on the page below the camera

![PowerApps Insert Gallery](docs-images/powerapps-insert-gallery.JPG)

In order for the application to know which pictures to use we reuse the **myPics** variable we created in the Camera setup

On the properties pane, select **myPics** from the **Items** dropdown menu

![PowerApps Collection Images Setup](docs-images/powerapps-collection-images.JPG)

Now select a single image slot from the gallery and on the properties pane select the **Advanced** tab. Complete the code below for the correct fields:

* OnSelect: ``` Remove(myPics, ThisItem) ```
* Image: ``` ThisItem.Url ```

![PowerApps Remove Images Setup](docs-images/powerapps-remove-image.JPG)

Next we add a **Text Input** box from the **Text** menu on the insert tab. This box will allow us to give our image a name when we send it to Azure Blob Storage.

![PowerApps Insert Text Input](docs-images/powerapps-insert-text-input.JPG)

Align the **Text Input** box underneath the Camera and above the Image gallery

Finally add a **Button** to the page. This cna be found underneath the **Insert -> Controls -> Button** options

Place the button next to the text input box underneath the Camera

![PowerApps Insert Button](docs-images/powerapps-insert-button.JPG)

On the properties pane for the button change the **Text** field to **Send**

![PowerApps Button Properties](docs-images/powerapps-button-properties.JPG)

Now we need to add Azure Blob Storage as our data source. This will mean we can send the image taken by the camera in the app to storage and this will trigger our Logic app

Go to **View** in the main toolbar, then **Data Sources**. This will open a pane on the right where you can click **Add Data Source**

![PowerApps Add Data Source](docs-images/powerapps-add-datasource.JPG)

Select **New Connection** and search for **blob** in the search box. Then click the Azure Blob Storage option

![PowerApps Add Data Source setup connection](docs-images/powerapps-datasource-setup.JPG)

Insert the connection information for your Azure Blob Storage account you used in the Logic App scenario: example ainightsstor.

![PowerApps Add Data Source setup connection](docs-images/PowerApps-azure-blob-storage-connection.JPG)

Once authenticated you will then see your blob storage connection added to the connections pane

![PowerApps Data Added](docs-images/powerapps-data-added.JPG)

Now we can use this connection in a function. Click on the **Send** button and switch to the **Advanced** pane.

In the OnSelect box type: 
 ``` AzureBlobStorage.CreateFile("images", TextInput1.Text, Camera1.Photo) ```


![PowerApps Azure Blob Function](docs-images/powerapps-function.JPG)


Now we have built an app lets test it in our development environment. In the top right of the screen you will see the toolbar below - press the **Play** button highlighted. This will open a new window with your application running. This will ask for access to your camera to test the app

![PowerApps Preview your app](docs-images/powerapps-preview-app.JPG)

> Test you app by taking a picture of a dog (or anything at this point). The camera will take a picture - name it - click the send button. Once sent wait a moment and you should recieve an email as your Logic app will have triggered

![PowerApps Preview your app](docs-images/powerapps-preview-running.JPG)

Now we are going to **Save** and **Publish** the application so you can use it on your mobile device

Go to the **File** tab in to top toolbar and choose the option on the left pane **Save**. Then click the **save** button.

Once saved you will have the **Publish** button appear - select this

![PowerApps Publish](docs-images/powerapps-publish.JPG)

![PowerApps save](docs-images/powerapps-saved.JPG)

You can also edit the look of the icon for the application. In the **File** menu go to **App Settings**.

In **App Name and Icon** select a background color for your application and choose an icon. You can also upload you own. Why not add a dog icon? Download the icon from [here](sample-code/dog-icon.png) and choose the **browse** button to add your own icon

![PowerApps Change App Settings](docs-images/powerapps-app-settings.JPG)

In order to view your published app on your phone you will need to download the PowerApps app from your app store. 

> For this tutorial the instructions will be for IOS.

![PowerApps IPhone download](docs-images/powerapps-download.png)

Once the app is download. Open the application and log in with your organizational credentials. Once logged in you should see all your organizations apps listed

![PowerApps apps listed on phone](docs-images\PowerApps-in-PowerApps-on-phone.png)

For you Dog Spotter app we want to add it to your home screen like any other application. Click on the 3 dots (...) and select **pin to home**

![PowerApps Pin to home screen](docs-images/powerapps-pin-app.png)

This will open the web browser where you follow the instructions to add it to your home screen. Select the share button.

![PowerApps add to home screen](docs-images/powerapps-add-to-homescreen.png)

Select **Add to Home Screen**

![PowerApps add to home screen using IOS functionality](docs-images/powerapps-add-to-homescreen-button.png)

Provide your application useful name to be shown on your phone and select Add

![PowerApps Home Screen Details](docs-images/powerapps-homescreen-detail.png)

### Congratulations!!

The app is now added to your phone home screen and you can open and run the functionality.

Test the app by taking a picture of a dog and sending it to the cloud.
