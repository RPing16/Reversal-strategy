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

## 交易成本
台股目前券商手續費有優惠，普遍有6折，部分券商提供1~2.8折優惠。若以3折優惠計算:
- 手續費 : 0.1425%*0.3，買賣都收
- 證交稅 : 0.3%，賣出才收
- 買入交易成本 = 0.1425%*0.3 = 0.04275%
- 賣出交易成本 = 0.1425%*0.3 + 0.3% = 0.34275%
- total交易成本 = 0.3855%
- 平均total交易成本 = 0.19275%
- 本專案交易成本計算方式採「單邊0.2%」

## 內容摘要
1. **讀取並處理data**
2. **設計反轉策略**
3. **回測**
4. **報酬貢獻度分析**
5. **檢驗每日持股數量是否有成功固定住**
6. **參數最佳化**
7. **使用最佳參數生成分析圖表**

## 結論
- 期間 : 反轉策略中期表現最佳，中期略優於長期，遠由於短期
- 適用性 : 反轉策略在扣除交易成本後最大sharpe ratio = 0.37，績效不好，說明台股不適用反轉策略
  
## code重點說明
1. **rank**
- 在計算signal時，給予跌幅rank以轉換原始訊號 : 跌幅數值 -> 跌幅rank (跌幅愈大rank愈大)
- 用意 :
    - 使用原始信號分配權重可能發生權重過度集中在某幾個股票(離群值)
    - 為降低風險，將原始信號轉換成rank，如此一來，既保留原始訊號的大小順序關係，又可以控制住權重不會過度集中  
2. **signal**
- signal>=0，signal>0買進持有，signal=0不持有。signal>0的幅度愈大，持有權重愈大
3. **normalize**
- 計算每日股票持有權重時進行標準化，依據當日跌幅rank進行加權
4. **參數最佳化 - days**
- 使用不同參數days，尋找哪個days使策略sharpe ratio極大
- 結果 : 反轉策略中期表現最佳，中期略優於長期，遠由於短期

## 策略績效分析圖表
![示例圖片](https://github.com/RPing16/Reversal-strategy/blob/main/Strategic%20Performance%20Analysis%20Chart/cum%20ret%20line%20chart.jpg)

![示例圖片](https://github.com/RPing16/Reversal-strategy/blob/main/Strategic%20Performance%20Analysis%20Chart/key%20performance%20table.jpg)

![示例圖片](https://github.com/RPing16/Reversal-strategy/blob/main/Strategic%20Performance%20Analysis%20Chart/EOY%20Returns%20vs%20Benchmark.jpg)

![示例圖片](https://github.com/RPing16/Reversal-strategy/blob/main/Strategic%20Performance%20Analysis%20Chart/rolling%20index.jpg)
