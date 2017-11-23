---
title: "说明 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4846a576-57ea-4068-959c-81e69e39ddc1
caps.latest.revision: "13"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 3aa20ea08fe34eab316a41d46ea955a78e4be512
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="explain-transact-sql"></a>说明 (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  返回的查询计划[!INCLUDE[ssDW](../../includes/ssdw-md.md)][!INCLUDE[DWsql](../../includes/dwsql-md.md)]而无需运行该语句的语句。 使用**说明**对哪些操作需要数据移动的预览并查看查询操作的估计的成本。  
  
 有关查询计划的详细信息，请参阅"了解查询计划"中[!INCLUDE[pdw-product-documentation_md](../../includes/pdw-product-documentation-md.md)]。  
  
## <a name="syntax"></a>语法  
  

```  
EXPLAIN SQL_statement  
[;]  
```  
  
## <a name="arguments"></a>参数  
 *SQL_statement*  
 [!INCLUDE[DWsql](../../includes/dwsql-md.md)]语句在其上的**说明**将运行。 *SQL_statement*可以是任何这些命令：**选择**，**插入**，**更新**，**删除**， **CREATE TABLE AS SELECT**，**创建远程表**。  
  
## <a name="permissions"></a>Permissions  
 需要**SHOWPLAN**权限和执行权限*SQL_statement*。 请参阅[权限： GRANT、 DENY、 REVOKE 和 #40;Azure SQL 数据仓库、 并行数据仓库和 #41;](../../t-sql/statements/permissions-grant-deny-revoke-azure-sql-data-warehouse-parallel-data-warehouse.md).  
  
## <a name="return-value"></a>返回值  
 中的返回值**说明**命令为下面所示的结构具有的 XML 文档。 此 XML 文档列出给定查询的查询计划中的所有操作，每个括`<dsql_operation>`标记。 返回值的类型是**nvarchar (max)**。  
  
 返回的查询计划描述了顺序的 SQL 语句;运行查询时它可能涉及到并行化的操作，因此某些所示的顺序语句可能会在同一时间运行。  
  
```  
\<?xml version="1.0" encoding="utf-8"?>  
<dsql_query>  
  <sql>. . .</sql>  
  <params />  
  <dsql_operations>  
    <dsql_operation>  
     . . .      
    </dsql_operation>  
    [ . . . n ]  
  <dsql_operations>  
</dsql_query>  
```  
  
 XML 标记包含此信息：  
  
|XML 标记|摘要、 属性和内容|  
|-------------|--------------------------------------|  
|\<dsql_query >|顶级级别/文档元素。|
|\<sql >|回显*SQL_statement*。|  
|\<params >|这次不使用此标记。|  
|\<dsql_operations >|总结了和包含的查询步骤中，并包括查询的成本信息。 此外包含的所有`<dsql_operation>`块。 此标记包含整个查询的计数信息：<br /><br /> `<dsql_operations total_cost=total_cost total_number_operations=total_number_operations>`<br /><br /> *total_cost*是查询后，若要运行，以毫秒为单位的总估计的时间。<br /><br /> *total_number_operations*是查询的操作的总数目。 将并行化和多个节点上运行的操作将计为单个操作。|  
|\<dsql_operation >|描述查询计划中的单个操作。 \<Dsql_operation > 标记中包含的操作类型作为特性：<br /><br /> `<dsql_operation operation_type=operation_type>`<br /><br /> *operation_type*是中找到的值之一[查询数据 (SQL Server PDW)](http://msdn.microsoft.com/en-us/3f4f5643-012a-4c36-b5ec-691c4bbe668c)。<br /><br /> 中的内容`\<dsql_operation>`块均依赖于操作类型。<br /><br /> 请参阅下表。|  
  
|操作类型|内容|示例|  
|--------------------|-------------|-------------|  
|BROADCAST_MOVE、 DISTRIBUTE_REPLICATED_TABLE_MOVE、 MASTER_TABLE_MOVE、 PARTITION_MOVE、 SHUFFLE_MOVE 和 TRIM_MOVE|`<operation_cost>`具有这些属性的元素。 值反映仅本地操作：<br /><br /> -   *成本*本地运算符成本，并显示操作后，若要运行，以毫秒为单位的估计的时间。<br />-   *accumulative_cost*是包括以毫秒为单位的总和的值的并行操作中，计划中看到的所有操作的总和。<br />-   *average_rowsize*是行检索和操作期间传递的估计平均行大小 （以字节为单位）。<br />-   *output_rows*输出 （节点） 基数，并显示输出行数。<br /><br /> `<location>`： 的节点或该操作将在其中发生的分发。 选项为:"控制"、"ComputeNode"、"AllComputeNodes"、"AllDistributions"、"SubsetDistributions"、"分发"和"SubsetNodes"。<br /><br /> `<source_statement>`： 随机排布源数据移动。<br /><br /> `<destination_table>`： 这些数据将移到内部临时表。<br /><br /> `<shuffle_columns>`: （适用于 SHUFFLE_MOVE 操作仅)。 将用作临时表分布列的一个或多个列。|`<operation_cost cost="40" accumulative_cost="40" average_rowsize = "50" output_rows="100"/>`<br /><br /> `<location distribution="AllDistributions" />`<br /><br /> `<source_statement type="statement">SELECT [TableAlias_3b77ee1d8ccf4a94ba644118b355db9d].[dist_date] FROM [qatest].[dbo].[flyers] [TableAlias_3b77ee1d8ccf4a94ba644118b355db9d]       </source_statement>`<br /><br /> `<destination_table>Q_[TEMP_ID_259]_[PARTITION_ID]</destination_table>`<br /><br /> `<shuffle_columns>dist_date;</shuffle_columns>`|  
|CopyOperation|`<operation_cost>`： 请参阅`<operation_cost>`上面。<br /><br /> `<DestinationCatalog>`： 目标或多个节点。<br /><br /> `<DestinationSchema>`: 在 DestinationCatalog 目标架构。<br /><br /> `<DestinationTableName>`:"表名"的目标表的名称。<br /><br /> `<DestinationDatasource>`： 目标数据源名称或连接信息。<br /><br /> `<Username>`和`<Password>`： 这些字段指示的用户名和密码目标可能是必需。<br /><br /> `<BatchSize>`： 复制操作批大小。<br /><br /> `<SelectStatement>`: 用于执行复制的 select 语句。<br /><br /> `<distribution>`： 在其中执行复制分发。|`<operation_cost cost="0" accumulative_cost="0" average_rowsize="4" output_rows="1" />`<br /><br /> `<DestinationCatalog>master</DestinationCatalog>`<br /><br /> `<DestinationSchema>dbo</DestinationSchema>`<br /><br /> `<DestinationTableName>[TableName]</DestinationTableName>`<br /><br /> `<DestinationDatasource>localhost, 8080</DestinationDatasource>`<br /><br /> `<Username>...</Username>`<br /><br /> `<Password>...</Password>`<br /><br /> `<BatchSize>6000</BatchSize>`<br /><br /> `<SelectStatement>SELECT T1_1.c1 AS c1 FROM [qatest].[dbo].[gigs] AS T1_1</SelectStatement>`<br /><br /> `<distribution>ControlNode</distribution>`|  
|MetaDataCreate_Operation|`<source_table>`： 该操作源表。<br /><br /> `<destionation_table>`： 该操作目标表。|`<source_table>databases</source_table>`<br /><br /> `<destination_table>MetaDataCreateLandingTempTable</destination_table>`|  
|ON|`<location>`： 请参阅`<location>`上面。<br /><br /> `<sql_operation>`： 标识将在节点执行的 SQL 命令。|`<location permanent="false" distribution="AllDistributions">Compute</location>`<br /><br /> `<sql_operation type="statement">CREATE TABLE [tempdb].[dbo]. [Q_[TEMP_ID_259]]_ [PARTITION_ID]]]([dist_date] DATE) WITH (DISTRIBUTION = HASH([dist_date]),) </sql_operation>`|  
|RemoteOnOperation|`<DestinationCatalog>`： 目标目录。<br /><br /> `<DestinationSchema>`: 在 DestinationCatalog 目标架构。<br /><br /> `<DestinationTableName>`:"表名"的目标表的名称。<br /><br /> `<DestinationDatasource>`： 目标数据源的名称。<br /><br /> `<Username>`和`<Password>`： 这些字段指示的用户名和密码目标可能是必需。<br /><br /> `<CreateStatement>`： 目标数据库表创建语句。|`<DestinationCatalog>master</DestinationCatalog>`<br /><br /> `<DestinationSchema>dbo</DestinationSchema>`<br /><br /> `<DestinationTableName>TableName</DestinationTableName>`<br /><br /> `<DestinationDatasource>DestDataSource</DestinationDatasource>`<br /><br /> `<Username>...</Username>`<br /><br /> `<Password>...</Password>`<br /><br /> `<CreateStatement>CREATE TABLE [master].[dbo].[TableName] ([col1] BIGINT) ON [PRIMARY] WITH(DATA_COMPRESSION=PAGE);</CreateStatement>`|  
|RETURN|`<resultset>`： 结果集标识符。|`<resultset>RS_19</resultset>`|  
|RND_ID|`<identifier>`： 创建的对象标识符。|`<identifier>TEMP_ID_260</identifier>`|  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
 **解释**可应用于*可优化*仅，查询，该查询可以改进或修改的查询的结果基于**解释**命令。 支持**说明**命令上面所列。 尝试使用**说明**与不受支持的查询类型将返回错误或回显查询。  
  
 **解释**不支持在用户事务中。  
  
## <a name="examples"></a>示例  
 下面的示例演示**说明**命令在上运行**选择**语句和 XML 结果。  
  
 **提交的 EXPLAIN 语句**  
  
 此示例的提交的命令是：  
  
```  
-- Uses AdventureWorks  
  
EXPLAIN   
    SELECT CAST (AVG(YearlyIncome) AS int) AS AverageIncome,   
        CAST(AVG(FIS.SalesAmount) AS int) AS AverageSales,   
        G.StateProvinceName, T.SalesTerritoryGroup  
    FROM dbo.DimGeography AS G  
    JOIN dbo.DimSalesTerritory AS T  
        ON G.SalesTerritoryKey = T.SalesTerritoryKey  
    JOIN dbo.DimCustomer AS C  
        ON G.GeographyKey = C.GeographyKey  
    JOIN dbo.FactInternetSales AS FIS  
        ON C.CustomerKey = FIS.CustomerKey  
    WHERE T.SalesTerritoryGroup IN ('North America', 'Pacific')  
        AND Gender = 'F'  
    GROUP BY G.StateProvinceName, T.SalesTerritoryGroup  
    ORDER BY AVG(YearlyIncome) DESC;  
GO  
```  
  
 执行语句使用后**说明**选项，消息选项卡显示单个行标题为**解释**，，然后使用 XML 文本启动`\<?xml version="1.0" encoding="utf-8"?>`单击以打开中的整个文本的 XMLXML 窗口。 若要更好地了解以下注释，你应打开 SSDT 中的行号显示的选项。  
  
#### <a name="to-turn-on-line-numbers"></a>若要打开行号  
  
1.  输出显示在**解释**选项卡上的 SSDT，**工具**菜单上，选择**选项**。  
  
2.  展开**文本编辑器**部分中，展开**XML**，然后单击**常规**。  
  
3.  在**显示**区域中，检查**行号**。  
  
4.  单击 **“确定”**。  
  
 **示例解释输出**  
  
 XML 结果**说明**了开启的行号命令：  
  
```  
1  \<?xml version="1.0" encoding="utf-8"?>  
2  <dsql_query>  
3    <sql>SELECT CAST (AVG(YearlyIncome) AS int) AS AverageIncome,   
4          CAST(AVG(FIS.SalesAmount) AS int) AS AverageSales,   
5          G.StateProvinceName, T.SalesTerritoryGroup  
6      FROM dbo.DimGeography AS G  
7      JOIN dbo.DimSalesTerritory AS T  
8          ON G.SalesTerritoryKey = T.SalesTerritoryKey  
9      JOIN dbo.DimCustomer AS C  
10          ON G.GeographyKey = C.GeographyKey  
11      JOIN dbo.FactInternetSales AS FIS  
12          ON C.CustomerKey = FIS.CustomerKey  
13      WHERE T.SalesTerritoryGroup IN ('North America', 'Pacific')  
14          AND Gender = 'F'  
15      GROUP BY G.StateProvinceName, T.SalesTerritoryGroup  
16      ORDER BY AVG(YearlyIncome) DESC</sql>  
17    <dsql_operations total_cost="0.926237696" total_number_operations="9">  
18      <dsql_operation operation_type="RND_ID">  
19        <identifier>TEMP_ID_16893</identifier>  
20      </dsql_operation>  
21      <dsql_operation operation_type="ON">  
22        <location permanent="false" distribution="AllComputeNodes" />  
23        <sql_operations>  
24          <sql_operation type="statement">CREATE TABLE [tempdb].[dbo].[TEMP_ID_16893] ([CustomerKey] INT NOT NULL, [GeographyKey] INT, [YearlyIncome] MONEY ) WITH(DATA_COMPRESSION=PAGE);</sql_operation>  
25        </sql_operations>  
26      </dsql_operation>  
27      <dsql_operation operation_type="BROADCAST_MOVE">  
28        <operation_cost cost="0.121431552" accumulative_cost="0.121431552" average_rowsize="16" output_rows="31.6228" />  
29        <source_statement>SELECT [T1_1].[CustomerKey] AS [CustomerKey],  
30         [T1_1].[GeographyKey] AS [GeographyKey],  
31         [T1_1].[YearlyIncome] AS [YearlyIncome]  
32  FROM   (SELECT [T2_1].[CustomerKey] AS [CustomerKey],  
33                 [T2_1].[GeographyKey] AS [GeographyKey],  
34                 [T2_1].[YearlyIncome] AS [YearlyIncome]  
35          FROM   [AdventureWorksPDW2012].[dbo].[DimCustomer] AS T2_1  
36          WHERE  ([T2_1].[Gender] = CAST (N'F' COLLATE Latin1_General_100_CI_AS_KS_WS AS NVARCHAR (1)) COLLATE Latin1_General_100_CI_AS_KS_WS)) AS T1_1</source_statement>  
37        <destination_table>[TEMP_ID_16893]</destination_table>  
38      </dsql_operation>  
39      <dsql_operation operation_type="RND_ID">  
40        <identifier>TEMP_ID_16894</identifier>  
41      </dsql_operation>  
42      <dsql_operation operation_type="ON">  
43        <location permanent="false" distribution="AllDistributions" />  
44        <sql_operations>  
45          <sql_operation type="statement">CREATE TABLE [tempdb].[dbo].[TEMP_ID_16894] ([StateProvinceName] NVARCHAR(50) COLLATE Latin1_General_100_CI_AS_KS_WS, [SalesTerritoryGroup] NVARCHAR(50) COLLATE Latin1_General_100_CI_AS_KS_WS NOT NULL, [col] BIGINT, [col1] MONEY NOT NULL, [col2] BIGINT, [col3] MONEY NOT NULL ) WITH(DATA_COMPRESSION=PAGE);</sql_operation>  
46        </sql_operations>  
47      </dsql_operation>  
48      <dsql_operation operation_type="SHUFFLE_MOVE">  
49        <operation_cost cost="0.804806144" accumulative_cost="0.926237696" average_rowsize="232" output_rows="108.406" />  
50        <source_statement>SELECT [T1_1].[StateProvinceName] AS [StateProvinceName],  
51         [T1_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup],  
52         [T1_1].[col2] AS [col],  
53         [T1_1].[col] AS [col1],  
54         [T1_1].[col3] AS [col2],  
55         [T1_1].[col1] AS [col3]  
56  FROM   (SELECT ISNULL([T2_1].[col1], CONVERT (MONEY, 0.00, 0)) AS [col],  
57                 ISNULL([T2_1].[col3], CONVERT (MONEY, 0.00, 0)) AS [col1],  
58                 [T2_1].[StateProvinceName] AS [StateProvinceName],  
59                 [T2_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup],  
60                 [T2_1].[col] AS [col2],  
61                 [T2_1].[col2] AS [col3]  
62          FROM   (SELECT   COUNT_BIG([T3_2].[YearlyIncome]) AS [col],  
63                           SUM([T3_2].[YearlyIncome]) AS [col1],  
64                           COUNT_BIG(CAST ((0) AS INT)) AS [col2],  
65                           SUM([T3_2].[SalesAmount]) AS [col3],  
66                           [T3_2].[StateProvinceName] AS [StateProvinceName],  
67                           [T3_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
68                  FROM     (SELECT [T4_1].[SalesTerritoryKey] AS [SalesTerritoryKey],  
69                                   [T4_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
70                            FROM   [AdventureWorksPDW2012].[dbo].[DimSalesTerritory] AS T4_1  
71                            WHERE  (([T4_1].[SalesTerritoryGroup] = CAST (N'North America' COLLATE Latin1_General_100_CI_AS_KS_WS AS NVARCHAR (13)) COLLATE Latin1_General_100_CI_AS_KS_WS)  
72                                    OR ([T4_1].[SalesTerritoryGroup] = CAST (N'Pacific' COLLATE Latin1_General_100_CI_AS_KS_WS AS NVARCHAR (7)) COLLATE Latin1_General_100_CI_AS_KS_WS))) AS T3_1  
73                           INNER JOIN  
74                           (SELECT [T4_1].[SalesTerritoryKey] AS [SalesTerritoryKey],  
75                                   [T4_2].[YearlyIncome] AS [YearlyIncome],  
76                                   [T4_2].[SalesAmount] AS [SalesAmount],  
77                                   [T4_1].[StateProvinceName] AS [StateProvinceName]  
78                            FROM   [AdventureWorksPDW2012].[dbo].[DimGeography] AS T4_1  
79                                   INNER JOIN  
80                                   (SELECT [T5_2].[GeographyKey] AS [GeographyKey],  
81                                           [T5_2].[YearlyIncome] AS [YearlyIncome],  
82                                           [T5_1].[SalesAmount] AS [SalesAmount]  
83                                    FROM   [AdventureWorksPDW2012].[dbo].[FactInternetSales] AS T5_1  
84                                           INNER JOIN  
85                                           [tempdb].[dbo].[TEMP_ID_16893] AS T5_2  
86                                           ON ([T5_1].[CustomerKey] = [T5_2].[CustomerKey])) AS T4_2  
87                                   ON ([T4_2].[GeographyKey] = [T4_1].[GeographyKey])) AS T3_2  
88                           ON ([T3_1].[SalesTerritoryKey] = [T3_2].[SalesTerritoryKey])  
89                  GROUP BY [T3_2].[StateProvinceName], [T3_1].[SalesTerritoryGroup]) AS T2_1) AS T1_1</source_statement>  
90        <destination_table>[TEMP_ID_16894]</destination_table>  
91        <shuffle_columns>StateProvinceName;</shuffle_columns>  
92      </dsql_operation>  
93      <dsql_operation operation_type="ON">  
94        <location permanent="false" distribution="AllComputeNodes" />  
95        <sql_operations>  
96          <sql_operation type="statement">DROP TABLE [tempdb].[dbo].[TEMP_ID_16893]</sql_operation>  
97        </sql_operations>  
98      </dsql_operation>  
99      <dsql_operation operation_type="RETURN">  
100        <location distribution="AllDistributions" />  
101        <select>SELECT   [T1_1].[col] AS [col],  
102           [T1_1].[col1] AS [col1],  
103           [T1_1].[StateProvinceName] AS [StateProvinceName],  
104           [T1_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup],  
105           [T1_1].[col2] AS [col2]  
106  FROM     (SELECT CONVERT (INT, [T2_1].[col], 0) AS [col],  
107                   CONVERT (INT, [T2_1].[col1], 0) AS [col1],  
108                   [T2_1].[StateProvinceName] AS [StateProvinceName],  
109                   [T2_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup],  
110                   [T2_1].[col] AS [col2]  
111            FROM   (SELECT CASE  
112                            WHEN ([T3_1].[col] = CAST ((0) AS BIGINT)) THEN CAST (NULL AS MONEY)  
113                            ELSE ([T3_1].[col1] / CONVERT (MONEY, [T3_1].[col], 0))  
114                           END AS [col],  
115                           CASE  
116                            WHEN ([T3_1].[col2] = CAST ((0) AS BIGINT)) THEN CAST (NULL AS MONEY)  
117                            ELSE ([T3_1].[col3] / CONVERT (MONEY, [T3_1].[col2], 0))  
118                           END AS [col1],  
119                           [T3_1].[StateProvinceName] AS [StateProvinceName],  
120                           [T3_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
121                    FROM   (SELECT ISNULL([T4_1].[col], CONVERT (BIGINT, 0, 0)) AS [col],  
122                                   ISNULL([T4_1].[col1], CONVERT (MONEY, 0.00, 0)) AS [col1],  
123                                   ISNULL([T4_1].[col2], CONVERT (BIGINT, 0, 0)) AS [col2],  
124                                   ISNULL([T4_1].[col3], CONVERT (MONEY, 0.00, 0)) AS [col3],  
125                                   [T4_1].[StateProvinceName] AS [StateProvinceName],  
126                                   [T4_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
127                            FROM   (SELECT   SUM([T5_1].[col]) AS [col],  
128                                             SUM([T5_1].[col1]) AS [col1],  
129                                             SUM([T5_1].[col2]) AS [col2],  
130                                             SUM([T5_1].[col3]) AS [col3],  
131                                             [T5_1].[StateProvinceName] AS [StateProvinceName],  
132                                             [T5_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
133                                    FROM     [tempdb].[dbo].[TEMP_ID_16894] AS T5_1  
134                                    GROUP BY [T5_1].[StateProvinceName], [T5_1].[SalesTerritoryGroup]) AS T4_1) AS T3_1) AS T2_1) AS T1_1  
135  ORDER BY [T1_1].[col2] DESC</select>  
136      </dsql_operation>  
137      <dsql_operation operation_type="ON">  
138        <location permanent="false" distribution="AllDistributions" />  
139        <sql_operations>  
140          <sql_operation type="statement">DROP TABLE [tempdb].[dbo].[TEMP_ID_16894]</sql_operation>  
141        </sql_operations>  
142      </dsql_operation>  
143    </dsql_operations>  
144  </dsql_query>  
  
```  
  
 **解释输出的含义**  
  
 上面的输出包含 144 带编号的行。 来自此查询的输出可能略有不同。 以下列表介绍重要部分。  
  
-   行 3 到 16 提供的所分析的查询的说明。  
  
-   行 17，指定操作的总数目将是 9。 你可以通过查看字样，找到的每个操作，开始**dsql_operation**。  
  
-   第 18 行启动操作 1。 第 18 和 19 行，则指示**RND_ID**操作将创建将用于对象说明的随机 ID 号。 上面的输出中所述的对象是**TEMP_ID_16893**。 你的号码将会不同。  
  
-   第 20 行启动操作 2。 行至第 25 的 21： 上所有计算节点，创建名为的临时表**TEMP_ID_16893**。  
  
-   行 26 启动操作 3。 行通过 37 27： 移动到的数据**TEMP_ID_16893**通过使用广播的移动。 提供发送给每个计算节点的查询。 行 37 指定目标表是**TEMP_ID_16893**。  
  
-   38 行启动操作 4。 行通过 40 39： 创建表的随机 ID。 **TEMP_ID_16894**是在上面的示例的 ID 编号。 你的号码将会不同。  
  
-   行 41 启动操作 5。 行通过 46 42： 在所有节点上创建名为的临时表**TEMP_ID_16894**。  
  
-   行 47 启动操作 6。 行 48 通过 91： 将数据从各种表移 (包括**TEMP_ID_16893**) 到表**TEMP_ID_16894**，通过使用随机排布移动操作。 提供发送给每个计算节点的查询。 行 90 指定目标表作为**TEMP_ID_16894**。 行 91年指定的列。  
  
-   行 92年启动操作 7。 通过 97 行 93年： 对所有计算节点、 删除临时表**TEMP_ID_16893**。  
  
-   行 98年启动操作 8。 通过 135 行 99年： 将结果返回到客户端。 使用查询来获取结果。  
  
-   行 136 启动操作 9。 行 137 到 140： 在所有节点上删除临时表**TEMP_ID_16894**。  
  
  

