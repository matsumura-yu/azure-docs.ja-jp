---
title: 'クイック スタート: テキスト スクリプトを変換する - Translator Text、Ruby'
titleSuffix: Azure Cognitive Services
description: このクイック スタートでは、Ruby で Translator Text API を使って 1 つの言語の中でテキストの表記を変換します。
services: cognitive-services
author: noellelacharite
manager: cgronlun
ms.service: cognitive-services
ms.component: translator-text
ms.topic: quickstart
ms.date: 06/22/2018
ms.author: nolachar
ms.openlocfilehash: 6595e486a93811fdded21050c39e99d4f7e5a760
ms.sourcegitcommit: f10653b10c2ad745f446b54a31664b7d9f9253fe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/18/2018
ms.locfileid: "46121755"
---
# <a name="quickstart-transliterate-text-with-ruby"></a>クイック スタート: Ruby を使ったテキストの表記変換

このクイック スタートでは、Translator Text API を使って、1 つの言語の中でテキストの表記を変換します。

## <a name="prerequisites"></a>前提条件

このコードを実行するには、[Ruby 2.4](https://www.ruby-lang.org/en/downloads/) 以降が必要です。

Translator Text API を使用するには、サブスクリプション キーも必要となります。「[Translator Text API にサインアップする方法](translator-text-how-to-signup.md)」を参照してください。

## <a name="transliterate-request"></a>表記変換要求

以下のコードは、[Transliterate](./reference/v3-0-transliterate.md) メソッドを使って、1 つの言語の中でテキストの表記を変換します。

1. 任意のコード エディターで新しい Ruby プロジェクトを作成します。
2. 次に示すコードを追加します。
3. `key` の値を、お使いのサブスクリプションで有効なアクセス キーに置き換えます。
4. プログラムを実行します。

```ruby
require 'net/https'
require 'uri'
require 'cgi'
require 'json'
require 'securerandom'

# **********************************************
# *** Update or verify the following values. ***
# **********************************************

# Replace the key string value with your valid subscription key.
key = 'ENTER KEY HERE'

host = 'https://api.cognitive.microsofttranslator.com'
path = '/transliterate?api-version=3.0'

# Transliterate text in Japanese from Japanese script (i.e. Hiragana/Katakana/Kanji) to Latin script.
params = "&language=ja&fromScript=jpan&toScript=latn";

uri = URI (host + path + params)

# Transliterate "good afternoon".
text = 'こんにちは'

content = '[{"Text" : "' + text + '"}]'

request = Net::HTTP::Post.new(uri)
request['Content-type'] = 'application/json'
request['Content-length'] = content.length
request['Ocp-Apim-Subscription-Key'] = key
request['X-ClientTraceId'] = SecureRandom.uuid
request.body = content

response = Net::HTTP.start(uri.host, uri.port, :use_ssl => uri.scheme == 'https') do |http|
    http.request (request)
end

result = response.body.force_encoding("utf-8")

json = JSON.pretty_generate(JSON.parse(result))
puts json
```

## <a name="transliterate-response"></a>表記変換応答

成功した応答は、次の例に示すように JSON で返されます。

```json
[
  {
    "text": "konnnichiha",
    "script": "latn"
  }
]
```

## <a name="next-steps"></a>次の手順

このクイック スタートをはじめとする各種ドキュメントで翻訳と言語認識を含んだサンプル コードを詳しく見てみましょう。GitHub にある Translator Text の各種サンプル プロジェクトもご覧ください。

> [!div class="nextstepaction"]
> [GitHub で Ruby のコード例を詳しく見てみる](https://aka.ms/TranslatorGitHub?type=&language=ruby)
