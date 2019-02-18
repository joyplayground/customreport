# 是什么

在日常开发中时长需要查看一些报表，比如pv uv，转化率等。而很多情况下，你并不需要晚上的BI系统来做这件事情。本自定义报表系统，尝试用一种简单的方式来解决这种问题。通过配置sql等来自动生成报表。

所以是一个可以高度自定义的报表生成系统。

# 不是什么

不是一个BI工具。不是一个数据分析引擎。

# 设计目标

1. 数据源灵活。可以适配各种类型的数据源。比如数据库，hive，hdfs，hbase，rest api等。
2. 数据源组合方便。报表数据来源可能会比较复杂。所以得能够把不同数据源的工具捏合在一起。
3. UI 免开发。不需要写报表代码即可完成UI展示工作。
4. 独立部署。可以根据自己的业务情况，选择合适的部署方案。

# 设计方案

> chat = present(model([format(fetch(datasource)), format(fetch(datasource, query))]), chatConfig)

1. datasource 数据源
2. fetch 从数据源获取数据
3. format 对获取到的数据进行处理
4. model 将多数据源组合成为model
5. present 绘制
6. chat 各种类型图标

变量配置： 

1. model 部分字段可以转换成为查询条件 query
2. 需要配置如何展示，chatConfig，比如同样的数据既可以展示成为柱状图，也可以展示成为折线图

核心对象：
1. model。通过对 model 字段的配置，来生成查询条件区域，来生成 query 对象，来生成具体类型的 chat。
2. chat。 不同类型的 chat 需要不同的 config 配置。chat 类型是预先定义好的若干种。

