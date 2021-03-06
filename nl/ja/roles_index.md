---

copyright:
  years: 2016, 2018
lastupdated: "2018-02-23"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# ユーザー、アプリケーション、ゲートウェイの役割

役割は、特定の操作へのアクセスを付与または制限するために使用可能な許可のセットです。 役割を使用して、ユーザー、アプリケーション、ゲートウェイのグループの許可を管理できます。
{:shortdesc}

## ユーザー役割
{: #user_roles}

{{site.data.keyword.iot_full}} にユーザーを追加、送信勧誘、または登録するときに、ユーザー役割を割り当てることができます。 また、{{site.data.keyword.iot_short_notm}} ダッシュボードを使用して、いつでもユーザー役割を割り当てまたは変更することができます。 ユーザーへの役割の割り当てについて詳しくは、[ユーザー役割の管理](managing_user_roles.html)を参照してください。

以下の標準的なユーザー役割を使用できます。

ユーザー役割 | 説明
------------- | -------------
管理者 | すべてのユーザー関連 API に対する権限を付与する「スーパーユーザー」役割。 管理者は、デバイスとアプリケーションに制限されている操作にアクセスできません。
オペレーター | フロントエンドの組織ユーザーを対象としています。 ほとんどの組織操作、アクセス制御操作、サード・パーティー操作、リスク管理操作に対する権限を付与します。
開発者 | デバイス操作、ログ操作、キャッシュ操作、ヒストリアン操作、サード・パーティー・サービス操作に対する無制限の権限を付与します。 この役割は、組織操作、アクセス制御操作、リスク管理操作に対する制限付き権限を付与します。
リーダー | デフォルトのユーザー役割。 すべてのユーザーが使用できる操作に対する制限付き権限を付与します。

ユーザー役割について詳しくは、[ユーザー役割](reference/roles_access.html)を参照してください。

## アプリケーション役割
{: #application_roles}
特定の操作に対する権限をアプリケーションに付与または拒否するアプリケーション役割を割り当てることができます。 すべてのアプリケーション役割は、以下の操作に対する権限を拒否します。

- すべてのリスク管理操作
- ストレージ・パラメーターの構成
- 認証プロバイダーの構成
- E メール構成の作成、更新、または削除

以下の標準的なアプリケーション役割を使用できます。

アプリケーション役割 | 説明
------------- | -------------
標準 | デフォルトのアプリケーション役割。 ほとんどのアプリケーション操作に対する権限を付与しますが、ユーザー操作と役割操作に対する権限は付与しません。   
操作 | 最も広い範囲の操作に対する権限を付与しますが、サブスクライブ操作とパブリッシュ操作に対する権限を拒否します。
バックエンド・トラステッド | システム・オペレーターに対して対話を要求しないアプリケーションを対象としています。 デバイス管理操作、組織操作、役割操作、または拡張機能操作に対する権限を拒否します。
データ・プロセッサー | 分析とデータ処理を実行するアプリケーションを対象としています。 データ・プロセッサー・アプリケーションには、組織操作とユーザー操作に対する制限付き権限が付与されます。
視覚化 | データ視覚化の生成を行うアプリケーションを対象としています。 視覚化アプリケーションには、ライブ・データと保管データの操作およびダッシュボード操作に対する権限があります。
デバイス | デバイスの役割を担うアプリケーションを対象としています。つまり、デバイスと同様に、{{site.data.keyword.iot_short_notm}} に送信されるデータの送信元になるアプリケーションのことです。 デバイス・アプリケーションには、操作に対する制限付き権限のみが付与されます。

アプリケーション役割の操作権限について詳しくは、[アプリケーション役割](reference/app_roles_access.html)を参照してください。

## ゲートウェイ役割
{: #gateway_roles}
ゲートウェイには、ゲートウェイの定義と {{site.data.keyword.iot_short_notm}} へのデバイスの登録機能を制御する少数の役割があります。

以下の標準的なゲートウェイ役割を使用できます。

ゲートウェイ役割 | 説明
------------- | -------------
標準 | 操作に対する制限付き権限が付与されます。 標準ゲートウェイは、そのゲートウェイに割り当てられているリソース・グループ内に含まれるデバイスの代わりに行う操作のみに動作が制限されます。
特権 | デフォルトのゲートウェイ役割。 信頼されたゲートウェイを対象としています。特権ゲートウェイは、デバイスを {{site.data.keyword.iot_short_notm}} に追加することができます。 デバイスとデバイス・プロパティーを追加、更新、管理する関連操作に対する権限を付与しますが、他の操作に対する権限はありません。  

ゲートウェイ役割の操作権限について詳しくは、[ゲートウェイ役割](reference/gateway_roles_access.html)を参照してください。
