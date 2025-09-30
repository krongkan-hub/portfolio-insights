# API Contract v0 (Web only, no Excel)

## GET /api/health
200: { "status": "ok" }

## GET /api/tickers
Res: [ { "symbol":"NVDA","name":"NVIDIA","last":123.45,"changePct":0.56 } ]

## GET /api/portfolio
Res: {
  "value": 123456.78,
  "pl_abs": 3456.78,
  "pl_pct": 2.88,
  "wtd_pct": 0.9,
  "mtd_pct": 3.1,
  "benchmarks": {"SPX": 0.5, "NDX": 0.8},
  "weights": [ { "symbol":"NVDA","weight":0.22 }, { "symbol":"AAPL","weight":0.18 } ]
}

## GET /api/tickers/{symbol}/signals?tf=1d|1h
Res: {
  "symbol":"NVDA","tf":"1d",
  "indicators":{
    "ema": {"20": 123.4, "50": 120.1},
    "macd": {"macd":0.45,"signal":0.30,"hist":0.15},
    "rsi": 58.7,
    "stoch": {"k":78.1,"d":74.3},
    "lrc": {"slope":0.012,"upper":130.2,"lower":118.4}
  },
  "signal":"HOLD"
}

## GET /api/tickers/{symbol}/series?interval=1d|1h
Res: { "symbol":"NVDA","interval":"1d",
  "series":[ {"t":"2025-09-01","c":120.1}, {"t":"2025-09-02","c":121.3} ] }

## POST /api/transactions
Body: { "date":"2025-09-01","symbol":"NVDA","side":"BUY","qty":10,"price":120,"fee":0 }
201: { "id": 1 }   |   400: { "error":"validation_error", "details":{...} }

## Error format
{ "error":"<code>", "message":"readable message" }