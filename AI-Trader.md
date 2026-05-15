---
created: 2026-05-12
updated: 2026-05-14
tags: [股票, AI-Trader, 模擬倉]
---

# AI-Trader 模擬倉

## 帳戶
- Agent：HermesV（ID: 6092）
- Cash：$93,393

## 持倉
| 股票 | 數量 | 成本 | 現價 | RSI | 52W高位 | 盈虧 | SL |
|------|------|------|------|-----|---------|------|-----|
| FCX | 100 | $63.03 | $66.14 | 62.5 | $70.97 | +$311 (+4.9%) | $61.46 (ATR×β) |

## Cron Job
| 時間 | Job ID |
|------|--------|
| 21:30 | 8cdc4b39c504 |
| 23:00 | d656b4abbbb3 |
| 01:00 | a11747f9609d |
| 03:00 | 521134c92920 |
| 03:30 | c1241db4e399 |

## 策略 Script
`/tmp/ai_trader_scan.py` — Stage 2 breakout + MA20 exit

## Entry（買入條件）
- above_ma20 = True
- stars >= 4
- RSI 25-75
- rr_ratio >= 0.8
- macd_hist > 0
- kdj_bull

## Exit（賣出條件）
- 跌穿止蝕位（5% / ATR×β）
- 收市價 < MA20（MA20追踪止賺）
- RSI > 70 + 遠高於MA50 → 考慮走一半
- Stars < 3 → 考慮走

## 止蝕位計算
- 固定5%：price × 0.95
- ATR×β：price - 1.5 × ATR × max(beta, 0.5)
- 取兩者中更低（更保守）

## 股票池
AI算力: IREN, CIFR, WULF, CORZ, NBIS, CRWV
網絡設備: ANET, MRVL
太空: ASTS, RKLB
核電/電網: VRT, CEG, OKLO
機械人: PATH, SYM
軍工: KTOS, AVAV
藍籌: AAPL, MSFT, GOOGL, AMZN, META, NVDA, TSLA, AVGO, AMD, ARM, CRM, ORCL, CSCO, ADBE, INTC, IBM, QCOM, TXN, AMAT, LRCX, SMCI, MU
中概: BIDU, JD, PDD, BABA, NTES, TSM, FUTU
金融: JPM, BAC, WFC, GS, MS, AXP
工業: CAT, DE, BA, LMT, RTX, HON, ONDS
消費: WMT, COST, HD, LOW, TGT, ROST
醫藥: UNH, JNJ, LLY, PFE, ABBV, MRK, TMO, DHR
能源: XOM, CVX, COP, MP, UUUU, FCX, AA
其他: DIS, CMCSA, VZ, T, PYPL, SQ, HOOD, SNDK, ALAB, GLDM, NVT, NOK
