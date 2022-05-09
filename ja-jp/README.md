# はじめに
![MobSF](https://cloud.githubusercontent.com/assets/4301109/20019521/cc61f7fc-a2f2-11e6-95f3-407030d9fdde.png)
Mobile Security Framework(MobSF)は、静的および動的分析を実行できる、自動化されたオールインワンのモバイルアプリケーション(Android/iOS/Windows)のペンテスト、マルウェア分析、およびセキュリティ評価フレームワークです。

### プロジェクト開発者

[Ajin Abraham](https://in.linkedin.com/in/ajinabraham) ![india](https://user-images.githubusercontent.com/4301109/37564171-6549d678-2ab6-11e8-9b9d-21327c7f5d5b.png) | [Magaofei](https://github.com/magaofei) ![china](https://user-images.githubusercontent.com/4301109/44515364-00bbe880-a6e0-11e8-944d-5b48a86427da.png) | [Matan Dobrushin](https://github.com/matandobr) ![israel](https://user-images.githubusercontent.com/4301109/37564177-782f1758-2ab6-11e8-91e5-c76bde37b330.png) | [Vincent Nadal](https://github.com/superpoussin22) ![france](https://user-images.githubusercontent.com/4301109/37564175-71d6d92c-2ab6-11e8-89d7-d21f5aa0bda8.png)


### MobSFを支援する

[![MobSFへの寄付](https://user-images.githubusercontent.com/4301109/117404264-7aab5480-aebe-11eb-9cbd-da82d7346bb3.png)](https://opensecurity.in/donate)

もしMobSFを気に入って役に立つと感じるなら、寄付を検討してください。


### MobSF eラーニングコースおよび認定

MobSFおよびその他のAndroidセキュリティツールをカバーする、自己学習形式のe-ラーニングコースが二つあります。

![MobSFコース](https://user-images.githubusercontent.com/4301109/76344880-ad68b580-62d8-11ea-8cde-9e3475fc92f6.png) [MobSFによる自動化されたモバイルアプリケーションセキュリティ分析 - MAS](https://opsecx.com/index.php/product/automated-mobile-application-security-assessment-with-mobsf/)

![Androidセキュリティツールコース](https://user-images.githubusercontent.com/4301109/76344939-c709fd00-62d8-11ea-8208-774f1d5a7c52.png) [Androidセキュリティツール専門家 -ATX](https://opsecx.com/index.php/product/android-security-tools-expert-atx/)


### MobSFのサポート

* **無償サポート:** 限定された無償のサポート、質問、ヘルプ、議論については、Slackチャンネルにご参加ください[![Join_MobSF_Slack](https://img.shields.io/badge/mobsf%20slack-join-green?logo=slack&labelColor=4A154B)](https://join.slack.com/t/mobsf/shared_invite/zt-153nfus2r-hMCGrwzm8Lyy3OxsihnolQ)
* **エンタープライズサポート:** 優先度の高い機能リクエスト、ライブサポート、オンライントレーニングについては以下を参照ください: [![MobSF Support Packages](https://img.shields.io/badge/enterprise-support%20package-blue?logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAGMAAABaCAMAAACbkBjCAAAAAXNSR0IB2cksfwAAAAlwSFlzAAALEwAACxMBAJqcGAAAAkNQTFRFAAAA////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////o1yoNQAAAMF0Uk5TAAQ1YH6IXzYFAUqq9P/1rU4CPdHWQ4X+jgOkro+hVWYR6vIajJvz+XN/z9sjLW6lrNPX+PsGHyE5TE9XWV1hW0k6LC7hs7SEhgr2sGRiFBCXJf38sgwOtmpoIiDf68vSGS+Z9yeR70RNvUEVfOa/WgdCR8XuUeeA8Du7Vporrx66SwlcqWV92g2HY+2Ki/GQJjxpM8TVcIGodjJ3ybETJOjUyiop4sxYkkVSGJ/pD6cdwlTOHNnIZ+B13bXkKL7NMOC0/xQAAAPPSURBVHic7dn5PxVRFADwY0sPN0t4Uj0vLQq9lkelRVFRKklZs+RRiiTtSbRoD9GuhdK+Ky3S9qf1Zu68bczcO5rjhz4f5yfnOud9mTszd+Y+gLH4f8PL28fXz893nP/4UQIMAYFBRIoJwSGho0CETSQeER6BLYRGGoksjFGTcIlouSDEZNRpmaJEEDIVkTApE4TEoBHmaWpG7HQsY4YaQchMJMI8S92IQ/pHZqsThMzBMeJZRgIKkcgiCJmLYcSwDQuGMY9tzMcwFrCNhQiEl5VtJCXrNxaxCUIW6zf8ecYS/UYKz1iq31jGM5brN1bwDB/9RirPQFhDuMdqpX5jFc9I0W+k8Yww/UY6z1it3zDzDLN+A9awiTUIBKxlGxkYRibbWIdhLGUbCLcrgPUTWETWegyDPSEbUAjYyDI24RjZWepE7GYcA3LUjSlIBGzJVSO2JmIZsG2UZ1wI1TUEYZ11RJ7KrFvz8Qy1S6QAkYBCZaMI0yhWNrZjGlCiRJSiElCmZJSPGWOGrtiheKFjGhW2yiVVO+XL+i6bz9pqHCB09x77B9YA1O6tcwHGffX7oYGQsnr9+2R5MeHiZx4QkmTTQSocsqUL+WHh5yNHs3UJxVHHpL87RBo5HphkbDwhvS770N9lNZ38Z6Gm2bXGmpyjLa7l1eI8cqdO/8tW7JmNHnutZ6XhtJzA1nOOx7bzbgUXLBdHKLRcKvU8iS4Lo2YL3de4cpXe1Ns8Sto7ro1A6AxMkl8KXQDXbc5tapLbuNsA0CSvumHy0gTkF96Ut9rjFtyWjRwFuDO8ruRuLVfoblLePLwH4bKRmwAFSpXW6E4WYC66rwjYw3fYY8MDgIMqxeWWh8qAobq1Uk0gJBJ6ej0GensAHqmWW1urDQoH6bE6YI82gD53pPeJvecpq+OZt5x4ztkJewEeSG+f0NTObIlL9SReDjtZZWEDd4QSoaqP2jRyX7kTr49wCPJGrKuqE5O34h0R3vGaYqvcjAxeNXlPC+k7biZNPnC7+l1EA7eYBNPKVjG5QxPuLgchH51GP79YetP/JCbxNDnOb5voIE7ya0kjvYboTSCInvsBGvocG5odGmrpkR2QsgF6vmvos0nGZw21X8TKCClrELOvGvq+UYK7SSwEnYIiKesSs0EtjXSl6dZSGi6WOr5ei3I7kTnRrd34LpYOSdmQmL1ANn6IpQlSRr+8mYpsiK9MyY672lbx4acZ2WgXKp84059C+gvZsAqVrt0ycWPsN7JhNHicrIPus6PBMJu0hPAcWOHM/giNKVr6zDAWI4i/nmw15nhs85kAAAAASUVORK5CYII=)](https://opensecurity.in/#support)



***
