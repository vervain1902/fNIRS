# 说明
- 脚本的目的是对fNIRS数据进行预处理和单脑激活检验
## 1 tableclean
- 规整原始数据，删除多余的行列（包括删除前后150个采样点），使其成为仅包含实验阶段的数据文件
- 降采样，对采样率为50Hz的数据降到10Hz
- 拆分被试，因每个原始数据包含2名被试的数据
- 数据文件以sub01到sub10命名，保存在mydata文件夹
## 2 datapreprocess
- 按照离群值的比例，逐通道逐被试检查数据质量，离群值比例大于5%的为坏通道，坏通道数量大于30%的为坏被试
- 以相邻好通道的数据替换坏通道的数据，保存在filterdata文件夹
- 原始数据可视化
- 带通滤波（BandpassFilter）、运动伪迹校正（MotionCorrect）、全局噪声去除（PCA）
- 图像和处理后的数据保存在filterdata文件夹
## 3 tablesplit
- 按实验阶段切分数据文件
	1. rest 静息
	2. think 思考
	3. talk 讨论
	4. share1 汇报1
	5. share2 汇报2
	6. share3 汇报3 
	7. listen 讲授
- xlsx和mat数据保存在splitdata文件夹
## 4 ttest
- 逐被试逐通道检验任务态（除了rest外所有阶段）与静息态的激活差异
- 逐被试按通道平均值检验任务态与静息态的激活差异
- 结果保存在ttest文件夹

---
## note
- adjmatrix文件为通道的相邻矩阵，1表示两通道相邻，0表示不相邻，该文件用于datapreprocess中的坏通道替换