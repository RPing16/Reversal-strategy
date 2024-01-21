# Reversal-strategy
將反轉策略應用於台股，每日買進過去D天跌幅最多的前X%的股票，權重依據當日跌幅進行加權
# files
1. **Reversal.ipynb**
- 動能策略code
2. **Strategy performance analysis.html**
- 動能策略績效分析
## data
- benchmark : 台灣加權股價指數(Y9999)調整後日報酬率，sources = TEJ
- strategy : 台灣上市上櫃公司調整後日報酬率，sources = TEJ
## 內容摘要
1. **讀取並處理data**
2. **設計反轉策略**
3. **回測**
4. **參數最佳化**
5. **其他分析**
    - 每日訊號數量(持有標的數量)
    - 選股方式 : 比例 -> 固定數量
## 結論
- 反轉策略在台股不適用
## code重點說明
1. **normalize**
- 計算每日股票持有權重時進行標準化，依據當日跌幅進行加權
2. **threshold**
- 閾值，買進跌幅前threshold%的股票
3. **signal**
- signal<=0，signal,0買進持有，signal=0不持有。signal<0的幅度愈大，持有權重愈大
4. **參數最佳化 - days**
- 使用不同參數days，尋找哪個days使策略報酬極大
- 結果 : 長期反轉策略績效明顯優於長期
5. **其他分析 : 比例->固定數量**
- 本project主要是採取買進『固定比例』的股票，因此當買進比例設定較大(threshold較小)時，會使得股票週轉率大幅增加 -> 交易成本大增 -> 策略報酬下降
- 因此，額外提供是以買進『固定數量』股票的code，透過降低股票週轉率降低交易成本
