---
created: 2026-05-12
updated: 2026-05-16
tags: [股票, AI-Trader, 模擬倉]
---

# AI-Trader 模擬倉

## 帳戶
- Agent：HermesV（ID: 6092）
- Cash：$5,808.05
- 總倉值：~$113,000（6倉）

## 持倉（2026-05-16 真實 API 數據）
| 股票 | 數量 | 成本 | 現價 | 盈虧 | PnL% | SL |
|------|------|------|------|------|------|----|
| ASTS | 100 | $77.56 | $83.67 | +$611 | +7.9% | $71.36 |
| CIFR | 126 | $20.31 | $20.33 | +$2 | +0.1% | $18.69 |
| NVT | 10 | $168.65 | $169.01 | +$4 | +0.2% | $155.16 |
| FCX | 534 | $65.07 | $63.01 | -$1,102 | -3.2% | $59.87 |
| AMD | 100 | $449.37 | $424.10 | -$2,527 | -5.6% | $413.42 |
| SMCI | 100 | $32.59 | $31.04 | -$155 | -4.8% | $29.98 |

**Cash: $4,660**

## 今日買入（03:30 scan）
- 2026-05-16: 買入 FCX @ $63.26 × 9（Stage 2 信號，累積共 534 股）
- 2026-05-16: 買入 CIFR @ $20.61 × 28（Stage 2 信號，累積共 126 股）

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
- RSI 20-80
- rr_ratio >= 0.8
- macd_hist > 0
- kd > -3

## Exit（賣出條件）
- **+20% 止賺 1/3**（先收割）
- **MA20 追踪止賺**（剩餘 2/3）
- 8% trailing stop（entry×0.92）→ 全走
- Stars < 3 → 考慮走

## ⚠️ Position Sizing 規則
- **每隻最多 10% 倉位**（總帳戶約 $120k → 每隻上限 ~$12k）
- 10% = ~120股 @ $100 嘅股票
- 堅決執行，唔可以因為信心大就all in

## 止蝕位計算（已過時）

## 止蝕位（新：8% trailing stop from entry）
- 入埗後止蝕位固定 = entry × 0.92
- 止蝕位只可上升，唔會下降
- 跌穿 entry×0.92 → 全走（8% 固定虧損）
- 例如：$100 入埗，SL = $92
- 舊：price × 0.95（已廢除，有bug）
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

## 歷史交易
- 2026-05-16: 買入 FCX @ $62.95 × 14（Stage 2 信號，累積共 514 股）
- 2026-05-16: 買入 CIFR @ $20.22 × 44（Stage 2 信號，累積共 98 股）
- 2026-05-14: 買入 ASTS @ $77.56 × 100（⭐5, RR=2.38）
- 2026-05-14: 買入 FCX @ $65.35 × 100（加倉，共500股）
- 2026-05-14: 買入 AMD @ $449.37 × 100（⭐5, RR=1.70）
- 2026-05-14: 買入 SMCI @ $32.59 × 100（⭐5, RR=1.48）
