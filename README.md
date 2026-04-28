Dataset_original_video加工中的四種狀態影片：
1.	Normal（正常）：標準的加工過程。
2.	Chatter（顫振）：加工時產生的異常震動。
3.	Rough cut（粗銑/粗加工）：大進給量的初步加工。
4.	Tool broken（刀具損壞）：刀具發生斷裂或嚴重磨損。

function1.ipynb
功能:熱力圖注意在加工刀具區域

第一階段
每隔5幀存一張圖，避免數據太過重複，並存成圖片檔(dataset)，供第二階段做訓練

第二階段
資料增強(用出更多樣的訓練資料)，採用resnet18將最後一層分類改成4個狀態，以防overfitting故設earlystopping

第三階段
實作:熱力圖權重疊加加工位置

結論
熱力圖（紅色區域）精準落在刀具與工件接觸的切削點上，模型透過觀察切削時產生的特徵（如切屑、火花或切削路徑）



function2.ipynb
功能:判斷在何種加工狀態

問題
根據TestMachining.mp4，將其標上狀態，如:Chatter , rough cut , Tool broken,etc.

方法:
step1:使用function1訓練好的模型，ResNet18 作為特徵提取器。

step2: while cap.isOpened()對每一幀做捕捉。

step3:避免狀態跳動頻繁，設buffer為10，紀錄最近出現最多次數作為顯示。

輸出為:marked_result_10resnet18.mp4
訓練好的權重:normal_ephos10_machining_model.pth
