## 数据管理规范

### [datahub](https://github.com/biominer-lab/datahub)
Datahub仓库用于管理本组织收集整理的所有数据集的Metadata，及制定的字段规范文档等。

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

### [cbioportal-datahub](https://github.com/biominer-lab/cbioportal-datahub)

<!--

**Here are some ideas to get you started:**

🙋‍♀️ A short introduction - what is your organization all about?
🌈 Contribution guidelines - how can the community get involved?
👩‍💻 Useful resources - where can the community find your docs? Is there anything else the community should know?
🍿 Fun facts - what does your team eat for breakfast?
🧙 Remember, you can do mighty things with the power of [Markdown](https://docs.github.com/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
-->
