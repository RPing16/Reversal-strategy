# Reversal strategy
將反轉策略應用於台股，每日買進過去D天跌幅最多的前N檔股票，權重依據當日跌幅進行加權

# files
1. **Reversal.ipynb**
- 反轉策略code
2. **Strategy performance analysis.html**
- 反轉策略績效分析code
3. **Strategic Performance Analysis Chart**
- 反轉策略績效分析圖表

## data
- benchmark : 台灣加權股價指數(Y9999)
- Strategy : 台灣所有上市上櫃公司
- 類別 : 報酬率資料
- 時間 : 2010/01/01 ~ 2023/06/30
- sources : TEJ

## 內容摘要
1. **讀取並處理data**
2. **設計反轉策略**
3. **回測**
4. **參數最佳化**
5. **檢驗每日持股數量是否有成功固定住**
6. **使用最佳參數生成分析圖表**

## 結論
- 期間 :反轉策略中長期優於短期，中期又略優於長期
- 適用性 : 反轉策略在扣除交易成本後最大sharpe ratio = 0.39，績效不好，說明台股不適用反轉策略
  
## code重點說明
1. **normalize**
- 計算每日股票持有權重時進行標準化，依據當日跌幅進行加權
2. **signal**
- signal>=0，signal>0買進持有，signal=0不持有。signal>0的幅度愈大，持有權重愈大
3. **參數最佳化 - days**
- 使用不同參數days，尋找哪個days使策略sharpe ratio極大
- 結果 : 反轉策略中長期優於短期，中期又略優於長期

## 策略績效分析圖表
