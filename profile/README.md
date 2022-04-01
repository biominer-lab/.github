# BioMiner计划
致力于打造一套集高质量多组学数据管理、分发与探索分析于一体的数据挖掘平台。

## For Users
Please access [the DataHub System](http://datahub.3steps.cn) to analyze and get omics data.

## For Dataset Reviewers

### [Datahub for The Cancer Omics Atlas](https://github.com/biominer-lab/datahub)

Datahub仓库用于管理本组织收集整理的肿瘤多组学数据集的Metadata及制定的字段规范文档等。

```
目录说明：
|- .github                   -> 存放持续集成与持续发布相关脚本文件，当仓库数据文件更新时触发系统将Metadata自动更新至Metabase
|- data                      -> 存放数据集关联的Metadata（每个项目一个子文件夹，每个子文件夹中包含若干实体描述文件，如project.csv，sample.csv等，具体参考规范文档）
|    |- FUSCC_LUAD
|    |       |- project.csv
|    |       |- ...
|    |       |- README.md
|    |- FUSCC_TNBC
|    |- FUSCC_CBCGA
|- docs                      -> 存放规范文档，含字段声明、管理模式、更新要求等
|- README.md                 -> 快速指南
|- CHANGELOG                 -> 数据集版本变更说明
|- LICENSE                   -> 版权声明文件
```

### [SEQC DataHub for Quality Control](https://github.com/biominer-lab/seqc-datahub)

SEQC Datahub仓库用于管理本组织收集整理的多组学质量控制相关数据集及制定的数据管理规范文档等

```
目录说明：
|- .github/                          -> 存放持续集成与持续发布相关脚本文件，当仓库数据文件更新时触发系统将Metadata自动更新至Metabase
|- data/                             -> 存放数据集关联的Metadata表格文件（每个项目一个子文件夹，每个子文件夹中包含若干实体描述文件，具体参考规范文档）
|    |- <标准物质名称>_RNA/
|    |       |- project/
|    |       |- donor/
|    |       |- biospecimen/
|    |       |- reference_materials/
|    |       |- library/
|    |       |- sequencing/
|    |       |- datafile/
|    |       |- README.md
|    |       |- CHANGELOG
|- docs/                             -> 存放规范文档，含字段声明、管理模式、更新要求等
|- README.md                         -> 快速指南
|- CHANGELOG                         -> 数据集版本变更说明
|- LICENSE                           -> 版权声明文件
```

### [cbioportal-datahub](https://github.com/biominer-lab/cbioportal-datahub)

## For Pipeline Developers

```mermaid
flowchart LR
  subgraph HPC [Testing on Local HPC]
    publications([Publications]) --Summarized by Pipeline Developer--> scripts[Pipeline with PBS Scripts]
    scripts --Evaluated by Pipeline Developer--> tested_pipeline[The Best Pipeline]
  end
  subgraph AliCloud [Running on AliCloud]
    app[Usable and Low-cost App] --Deployed by System Developer--> platform[ClinicoOmics Web System]
  end
  HPC -- Pipeline >>> App --> AliCloud
  HPC -. Developed by App Developer .-> AliCloud
```

## For System Developers

整套系统主要由以下部分组成：肿瘤多组学数据集、元数据QC & QA系统、标准化分析流程与系统、多组学数据管理系统（类似于Genomics Data Commons）、多组学数据探索分析系统（类似于cBioportal）

| 所属组成部分 | 过渡期软件系统  | 生产期软件系统 |功能描述                  |
|------------|----------|------------------|-------------------------|
| 肿瘤多组学数据集 | [DataHub (GitHub仓库)](https://github.com/biominer-lab/datahub)  | 同过渡期 |肿瘤多组学数据集管理       |
| 元数据QC & QA系统 | Metabase | 同过渡期 |元数据QC/QA |
| 标准化分析流程与系统 | SeqPipe  | 同过渡期 |原名Choppy Pipe, 标准化分析流程管理与运行 |
| 多组学数据管理系统 | Metabase + BioPoem + NODE/GSA/SRA + OSS | BioMiner + BioPoem (NODE/GSA/SRA + OSS) |Metabase - 多组学数据集相关元数据管理；<br/>Biopoem - 数据高速传输(测序公司 ---> 集群 ---> NODE ---> 阿里云/集群)；<br/>NODE/GSA/SRA - Level 1/2数据的存储；<br/>OSS - Level3数据的存储； |
| 多组学数据探索分析系统| cBioportal + [cBioportal DataHub](https://github.com/biominer-lab/cbioportal-datahub)  | BioMiner |cBioportal - 探索分析；<br/>cBioportal DataHub - 维护符合cBioportal规范要求的数据集；<br/>BioMiner - 多组学数据下游分析，支持两种分析模式：① 在线查询与实时探索分析（类似于cBioportal）② 统计与机器学习模块|

```mermaid
graph TD
    subgraph components
      BioMiner -- Manage <> Similar with GDC --> Metadata[Metadata];
      BioMiner -- Manage <> Similar with cBioportal --> AnalysisModules[Analysis Modules];
      Metadata -.- AnalysisModules;
    end

    Metadata -- Contains --> Info[Patient/Sample Information, etc.];
    Metadata -- File Link to --> Level1[Level1 Data - NODE/GSA/SRA];
    Metadata -- File Link to --> Level3[Level3 Data - Cloud Storage];
    Level1 -- Transfer to Cloud Storage by BioPoem & Convert Level1 Data to Level3 Data by SeqPipe  --> Level3;
    AnalysisModules -- Provides Modules --> DownstreamAnalysis[Downstream Analysis];
    Info -- Part of Dataset --> Dataset;
    Level3 -- Part of Dataset --> Dataset;
    Dataset -- Input Data --> DownstreamAnalysis(Mining Dataset with Several Analysis Modules on BioMiner);
    DownstreamAnalysis --> Kownledges;
    
    style Level1 fill:#00758f;
    style Level3 fill:#00758f;
    style Info fill:#00758f;
    style Metadata fill:#dafbe1;
    style AnalysisModules fill:#dafbe1;
```
