# Google Flights スクレイパー

[![Promo](https://github.com/luminati-io/LinkedIn-Scraper/blob/main/Proxies%20and%20scrapers%20GitHub%20bonus%20banner.png)](https://brightdata.jp/products/web-scraper/google-flights)

このリポジトリでは、Google Flights からフライトデータを抽出するための2つの方法を提供します。

1. **無料 Google Flights スクレイパー:** 小規模な抽出に最適です
2. **Google Flights スクレイパー API:** 大量かつリアルタイムのデータ抽出向けに設計されており、リクエスト数は無制限です。Bright Data の [SERP Scraping API](https://brightdata.jp/products/serp-api) の一部です。


## Table of Contents
2. [無料スクレイパー](#free-scraper)
   - [セットアップ要件](#setup-requirements)
   - [クイックスタート](#quick-start)
   - [サンプル出力](#sample-output)
   - [制限事項](#limitations)
3. [Google Flights スクレイパー API](#google-flights-api)
   - [主な機能](#key-features)
   - [前提条件](#prerequisites)
   - [Direct API アクセス](#direct-api-access)
   - [ネイティブのプロキシベースのアクセス](#native-proxy-based-access)
4. [追加パラメータ](#additional-parameters)
   - [ローカライゼーションパラメータ](#localization-parameters)
   - [通貨パラメータ](#currency-parameter)
5. [サポート＆リソース](#support--resources)

## 無料スクレイパー
Google Flights から限られたデータを抽出するための、手早くシンプルなスクレイパーです。

<img width="800" alt="google-flights-scraper" src="https://github.com/luminati-io/google-flights-api/blob/main/images/424383720-44ae10b1-4974-497e-9a7c-c1a762614f0e.png" />

### セットアップ要件
- [Python 3.9+](https://www.python.org/downloads/)
- ブラウザ自動化のための [Playwright](https://playwright.dev/)

```bash
pip install playwright
playwright install chromium
```

> **Webスクレイピングは初めてですか？** こちらの [Python で学ぶ Webスクレイピング入門ガイド](https://brightdata.jp/blog/how-tos/web-scraping-with-python) をご覧ください
>

### クイックスタート
1. [google-flights-scraper.py](https://github.com/luminati-io/google-flights-api/blob/main/google-flights-scraper/google-flights-scraper.py) を開きます
2. 次の変数を更新します:
    - `url`: Google Flights のURLを貼り付けます（通常 `tfs` を含みます）。
3. スクリプトを実行します。

💡 Pro Tip: Google のアンチスクレイピング対策による検知を最小化するために、`HEADLESS = False` に設定してください。

### サンプル出力
```json
{
  "airline": "Emirates",
  "departure_time": "4:15 AM",
  "arrival_time": "2:00 PM",
  "duration": "22 hr 15 min",
  "stops": "1 stop in DXB",
  "price": "$1,139",
  "co2_emissions": "1,092 kg CO2e",
  "emissions_variation": "+6% emissions"
}
```

👉  [完全な出力サンプルを見る](https://github.com/luminati-io/google-flights-api/blob/main/google-flights-results/flight_results.json)


### 制限事項
無料スクレイパーにはいくつかの制約があります:
- IPアドレスがブロックされるリスクが高いです
- リクエスト量が制限されます
- CAPTCHA が頻繁に発生します
- 本番利用には信頼性が不十分です

これらの制限なしで堅牢かつスケーラブルなスクレイピングを行うには、以下の Bright Data 専用APIをご検討ください。👇

## Google Flights スクレイパー API
[Bright Data の Google Flights スクレイパー API](https://brightdata.jp/products/web-scraper/google-flights) は [SERP Scraping API](https://brightdata.jp/products/serp-api) に統合されており、当社の広範な [プロキシネットワーク](https://brightdata.jp/proxy-types) を活用して、価格、スケジュール、航空会社の詳細などのリアルタイムなフライトデータを、CAPTCHA や IP ブロックなしで大規模に抽出します。

### 主な機能

- **グローバルな正確性:** 特定の場所に合わせた結果を提供します
- **Pay-Per-Success:** 成功したリクエストに対してのみ支払います
- **リアルタイムデータ:** 最新のフライトデータを数秒で取得します
- **無制限のスケーラビリティ:** 大量のスクレイピングを容易に処理します
- **コスト効率:** 高価なインフラが不要になります
- **信頼性の高いパフォーマンス:** ブロック回避技術を内蔵しています
- **24/7 専門サポート:** 必要なときにいつでも支援を受けられます

### 前提条件

1. [Bright Data アカウントを作成](https://brightdata.jp/) します（新規ユーザーには $5 のクレジットが付与されます）。
2. [API key](https://docs.brightdata.com/general/account/api-token) を生成します。
3. [ステップバイステップガイド](https://github.com/luminati-io/google-flights-api/blob/main/setup-serp-api-guide.md) に従って SERP API を設定し、認証情報をセットアップします。

### Direct API アクセス

API エンドポイントへ直接リクエストします。

**cURL 例:**

```bash
curl https://api.brightdata.com/request \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer API_TOKEN" \
  -d '{
        "zone": "ZONE_NAME",
        "url": "https://www.google.com/travel/flights/search?tfs=CBwQAhojEgoyMDI1LTA0LTAxagcIARIDREVMcgwIAxIIL20vMDRqcGxAAUgBcAGCAQsI____________AZgBAg",
        "format": "raw"
      }'
```

**Python 例:**

```python
import requests

url = "https://api.brightdata.com/request"
headers = {"Content-Type": "application/json", "Authorization": "Bearer API_TOKEN"}
payload = {
    "zone": "ZONE_NAME",
    "url": "https://www.google.com/travel/flights/search?tfs=CBwQAhojEgoyMDI1LTA0LTAxagcIARIDREVMcgwIAxIIL20vMDRqcGxAAUgBcAGCAQsI____________AZgBAg",
    "format": "raw",
}

response = requests.post(url, headers=headers, json=payload)

with open("google-flights-data.html", "w", encoding="utf-8") as file:
    file.write(response.text)
print("HTML response saved to 'google-flights-data.html'.")
```

### ネイティブのプロキシベースのアクセス

代わりに、Bright Data のプロキシルーティング方式を使用します。

**cURL 例:**

```bash
curl -i \
  --proxy brd.superproxy.io:33335 \
  --proxy-user "brd-customer-<customer-id>-zone-<zone-name>:<zone-password>" \
  -k \
  "https://www.google.com/travel/flights/search?tfs=CBwQAhojEgoyMDI1LTA0LTAxagcIARIDREVMcgwIAxIIL20vMDRqcGxAAUgBcAGCAQsI____________AZgBAg"
```

**Python 例:**

```python
import requests
import urllib3

urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)

host = "brd.superproxy.io"
port = 33335
username = "brd-customer-<customer-id>-zone-<zone-name>"
password = "<zone-password>"
proxy_url = f"http://{username}:{password}@{host}:{port}"

proxies = {"http": proxy_url, "https": proxy_url}
url = "https://www.google.com/travel/flights/search?tfs=CBwQAhojEgoyMDI1LTA0LTAxagcIARIDREVMcgwIAxIIL20vMDRqcGxAAUgBcAGCAQsI____________AZgBAg"
response = requests.get(url, proxies=proxies, verify=False)

with open("google-flights-data.html", "w", encoding="utf-8") as file:
    file.write(response.text)

print("Response saved to 'google-flights-data.html'.")
```

👉 [完全な HTML 出力](https://github.com/luminati-io/google-flights-api/blob/main/google-flights-api-output/google-flights-data.html) をご覧ください。

**注:** 本番利用では、[SSL Certificate Guide](https://docs.brightdata.com/general/account/ssl-certificate) に従って Bright Data の SSL 証明書を読み込んでください。


## 追加パラメータ
これらのオプションパラメータを使って、Google Flights のデータ抽出を微調整できます。

### ローカライゼーションパラメータ
<img width="800" alt="bright-data-google-flights-api-localization" src="https://github.com/luminati-io/google-flights-api/blob/main/images/424454961-e77f10c9-8e44-46aa-be3d-64c756741479.png" />

場所と言語に基づいて検索結果をカスタマイズします:

| Parameter | Description | Example |
| --- | --- | --- |
| gl | 2文字の国コード | `gl=us` (United States) |
| hl | 2文字の言語コード | `hl=en` (English) |


**例:** パリからロンドンへのフライトをフランス語で検索します:

```bash
curl --proxy brd.superproxy.io:33335 --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
"https://www.google.com/travel/flights/search?tfs=CBwQAhojEgoyMDI1LTA0LTAxagcIARIDQ0RHcgwIAxIIL20vMDRqcGxAAUgBcAGCAQsI____________AZgBAg&hl=fr&gl=fr"
```

### 通貨パラメータ

<img width="800" alt="bright-data-google-flights-api-currency" src="https://github.com/luminati-io/google-flights-api/blob/main/images/424820088-c571e99f-b854-449e-abc2-60149611ad5b.png" />

`curr` パラメータを使用して、返される価格の通貨を定義します。

**例:** 価格を USD で返します。

```bash
curl --proxy brd.superproxy.io:33335 --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
"https://www.google.com/travel/flights/search?tfs=CBwQAhojEgoyMDI1LTA0LTAxagcIARIDQ0RHcgwIAxIIL20vMDRqcGxAAUgBcAGCAQsI____________AZgBAg&hl=fr&gl=fr&curr=USD"
```

## サポート＆リソース

- **ドキュメント:** [SERP API Documentation](https://docs.brightdata.com/scraping-automation/serp-api/)
- **関連 API:** [Web Unlocker API](https://github.com/luminati-io/web-unlocker-api), [SERP API](https://github.com/luminati-io/serp-api), [Google Search API](https://github.com/luminati-io/google-search-api), [Google News Scraper](https://github.com/luminati-io/Google-News-Scraper), [Google Trends API](https://github.com/luminati-io/google-trends-api), [Google Reviews API](https://github.com/luminati-io/google-reviews-api), [Google Hotels API](https://github.com/luminati-io/google-hotels-api)
- **Google スクレイピングチュートリアル:**
    - [How to Scrape Google Flights](https://brightdata.jp/blog/web-data/how-to-scrape-google-flights)
    - [How to Scrape Google Search Results](https://brightdata.jp/blog/web-data/scraping-google-with-python)
    - [How to Scrape Google Maps](https://brightdata.jp/blog/web-data/how-to-scrape-google-maps)
- **ユースケース:**
    - [SEO & SERP Tracking](https://brightdata.jp/use-cases/serp-tracking)
    - [Travel Industry Data](https://brightdata.jp/use-cases/travel)
- **追加の読み物:** [Best SERP APIs](https://brightdata.jp/blog/web-data/best-serp-apis)
- **サポートへのお問い合わせ:** [support@brightdata.com](mailto:support@brightdata.com)