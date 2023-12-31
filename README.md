# RASA
This is a mentor bot that can help to solve the question, built with rasa framework and LLM. We design the bot with RAG strategy. when user ask a question in our scope. we will ask chatgpt with user's question and knowledge we perpared.


## Demo Dataset
Now we only use the first 3 topics to validate
```
Kc-Ⅳ-3-1	能知道磁鐵的發現科學史
Kc-Ⅳ-3-2	磁鐵的兩極為N極和S極，磁極間的磁力是一種超距力
Kc-Ⅳ-3-3	磁力線是假想線，可描述磁場的大小及方向
# Kc-Ⅳ-3-4	認識地球的磁場
# Kc-Ⅳ-4-1	厄斯特發現載有電流的導線會在其周圍建立磁場
# Kc-Ⅳ-4-2	能從實驗認識載有電流的長直導線周圍的磁場大小及方向
# Kc-Ⅳ-4-3	能從實驗認識載有電流的螺形線圈周圍的磁場大小及方向
# Kc-Ⅳ-4-4	安培定律：電流磁效應的強度與電流大小成正比，與距導線距離成反比
# Kc-Ⅳ-4-5	安培右手定則能說明電流磁效應的磁場方向
# Kc-Ⅳ-4-6	電流磁效應在生活中的應用_電磁鐵
# Kc-Ⅳ-4-7	電磁鐵在生活中的應用_電鈴、喇叭、傳統電話
# Kc-Ⅳ-5-1	以實驗認識載有電流的導線在磁場中會受力作用
# Kc-Ⅳ-5-2	能應用右手開掌定則舉例說明電流、磁場和受力方向
# Kc-Ⅳ-5-3	電流磁效應的應用_簡易馬達實驗
# Kc-Ⅳ-5-4	電流磁效應在生活中的應用_電動機的運作原理
# Kc-Ⅳ-6-1	能從實驗認識電磁感應的現象
# Kc-Ⅳ-6-2	法拉第定律:感應電流的大小和線圈中磁場變化速率成正比
# Kc-Ⅳ-6-3	能應用冷次定律推論感應流的方向
# Kc-Ⅳ-6-4	電磁感應的應用_發電機和變壓器
```

#### 單元對應的問題
```
- intent: faq/Kc-Ⅳ-3-1
  examples: |
    - 磁鐵的最早發現歷史可追溯至哪個時代或文明？
    - 有哪些早期的文化或科學家在磁鐵的研究與應用方面有顯著的貢獻？
    - 磁鐵的基本性質以及其在古代和現代的應用有哪些重要的科學發現？
- intent: faq/Kc-Ⅳ-3-2
  examples: |
    - 為什麼磁鐵的兩極被稱為N極和S極？
    - 什麼是磁極間的超距力，它是如何產生的？
    - 在日常生活中，我們可以舉出哪些例子來展示磁力的作用？
- intent: faq/Kc-Ⅳ-3-3
  examples: |
    - 磁力線如何協助我們理解磁場的特性？
    - 在物理世界中，磁力線的概念對於哪些領域或應用具有重要意義？
    - 請解釋磁力線的假想性質如何幫助科學家研究和應用磁場的知識。

```


# Service

### Start Service
- up service
```
docker-compose up
```

### Cowork with bot
- [Option 1] ask bot by cmd
```
curl -o output.txt -X POST -H "Content-Type: application/json; charset=UTF-8" -d '{"sender": "user-001","message": "早安"}'  http://127.0.0.1:5005/webhooks/rest/webhook && echo -e "$(<output.txt)"
curl -o output.txt -X POST -H "Content-Type: application/json; charset=UTF-8" -d '{"sender": "user-001","message": "昆蟲是甚麼?"}'  http://127.0.0.1:5005/webhooks/rest/webhook && echo -e "$(<output.txt)"
curl -o output.txt -X POST -H "Content-Type: application/json; charset=UTF-8" -d '{"sender": "user-001","message": "是的"}'  http://127.0.0.1:5005/webhooks/rest/webhook && echo -e "$(<output.txt)"
```

- [Option 2] by web

```
http://localhost:80/
```

# Testing
- wth rasa tests
```
docker-compose up test-model
```



----
# Backup

#### If you want to manually fintune
```
docker run --rm -it -v "actionsServer:/app" --name rasa -p 5005:5005 -p 5006:5006 --entrypoint /bin/bash rasa/rasa:3.6.6-full
```

or
```
docker run --rm -it -v ".actionsServer:/app" --name rasa -p 5005:5005 -p 5006:5006 --entrypoint /bin/bash rasa/rasa:3.6.6-full
```

or
```
docker exec -it rasa /bin/bash
```
