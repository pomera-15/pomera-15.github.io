+++
title = "ChatGPTのOpenAI APIを実行"
date = 2023-05-24T23:20:03+09:00
categories = [
    "llm",
]
Authors = "@pomera_15"
+++
### 1）参考
- openaiクイックスタート： https://platform.openai.com/docs/quickstart
- OpenAI APIレファレンス： https://platform.openai.com/docs/api-reference/introduction
- openai-python GitHub： https://github.com/openai/openai-python

&nbsp;
### 2）仮想環境の構築
```bash
% python3 -m venv chatgpt-venv      # 仮想環境の作成
% source chatgpt-venv/bin/activate  # 仮想環境の有効化
参考） % deactivate                  # 仮想環境の非有効化
```
&nbsp;
### 3）OpenAI APIの実行コード

準備：
```bash
% pip install openai
```
```bash
% export OPENAI_API_KEY="xxxxx"  # Keyを環境変数にセット
```
コード：
```python
import os
import openai

# organizationの設定
openai.organization = "xxxxx"

# Load your API key from an environment variable or secret management service
openai.api_key = os.getenv("OPENAI_API_KEY")

response = openai.Completion.create(
    model="text-davinci-003",  # モデルの指定
    prompt="こんにちは。お元気ですか？",  # 俗に言うプロンプト
    temperature=0,  # 出力の揺らぎ（0の場合、出力は固定される）
    max_tokens=100  # レスポンスの最大トークン数
    )

# レスポンスを出力
print(response)
```
&nbsp; 
### 4）実行結果

レスポンスは以下。

```bash
{
  "choices": [
    {
      "finish_reason": "stop",
      "index": 0,
      "logprobs": null,
      "text": "\n\n\u306f\u3044\u3001\u5143\u6c17\u3067\u3059\u3002\u3042\u308a\u304c\u3068\u3046\u3054\u3056\u3044\u307e\u3059\u3002"
    }
  ],
  "created": xxxxxxxxxx,
  "id": "xxxxxxxxxx",
  "model": "text-davinci-003",
  "object": "text_completion",
  "usage": {
    "completion_tokens": 25,
    "prompt_tokens": 19,
    "total_tokens": 44
  }
}
```

&nbsp; 
---
### 参考）エラー情報

- APIを叩いたが以下のエラーが出た。クレジットカード情報を登録していなかったためらしい。
```
openai.error.RateLimitError: You exceeded your current quota, please check your plan and billing details.
```
https://qiita.com/kotattsu3/items/d6533adc785ee8509e2c