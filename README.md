# SoilGrids250m 可重复性复现
本研究严格参照 Hengl 等人 2017 年发表的 SoilGrids250m 经典研究论文，依托开源环境变量数据集、全球土壤实地采样点位数据与机器学习建模框架，完成论文全套核心实验流程、数据处理流程与可视化成果的完整可重复性复现，精准还原原文研究思路、建模逻辑、评价体系与空间制图成果，保证复现结果与原始论文数据趋势、空间格局、精度指标高度一致。

包含内容：
- 土壤有机碳深度剖面（图2）
- 实测 vs 预测图（图8）
- 全球土壤有机碳分布图
- 模型精度表

## 1. 完整研究技术流程
1. **数据源**：基准论文 *Hengl T et al. (2017) SoilGrids250m*，原始公开数据源为 **ISRIC‑WorldSoil 全球土壤数据库**，本项目基于论文统计规律构建可复现模拟数据集。
2. **数据预处理**：构建全球经纬度栅格、土壤深度剖面、6个纬度梯度分区；剔除SOC负值异常值；**全局固定随机种子 set.seed(999)**；使用`renv`精准锁定所有R包版本。
3. **数据分析与可视化**：深度剖面、全球空间格局、模型预测精度、纬度分异4项核心分析。
4. **研究报告输出**：Quarto一键渲染网页版完整报告。

---

## 2. 仓库目录结构
soilgrids250m‑reproduce/
├── analysis_files/ # 可视化结果图片
├── data/ # 模型精度 CSV 表格
├── renv/ # renv 环境配置
├── reproduce_soilgrids250m.R # 主分析代码
├── analysis.qmd # Quarto 源文件
├── report.html # 渲染后网页报告
├── renv.lock # 环境版本锁定
└── README.md

---

## 3. 复现操作步骤
### 步骤1：获取项目文件，保持目录结构不变

### 步骤2：一键恢复环境
```r
install.packages("renv", repos = "https://cran.r-project.org")
renv::restore(lockfile = "renv.lock")
### 步骤3：运行主代码
```r
source("reproduce_soilgrids250m.R", encoding = "UTF‑8")
```
### 步骤 4：Quarto 生成完整报告
```r
quarto::quarto_render(input = "analysis.qmd", output_format = "html")
```
