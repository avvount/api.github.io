---
title: acme续期证书
date: 2021-06-19 16:14:29
tags:
---

```sh
acme.sh --issue -d example.cf -d "*.example.cf" --dns --yes-I-know-dns-manual-mode-enough-go-ahead-please --log

acme.sh --renew -d example.cf -d "*.example.cf" --yes-I-know-dns-manual-mode-enough-go-ahead-please --log
```
第一次执行会失败,需要去cloudflare上修改txt记录再重新执行一次