---
title: EXPLAIN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
ms.assetid: 4846a576-57ea-4068-959c-81e69e39ddc1
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 486d03addff39a0377298dcd1ddfb768046f2aa1
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2018
ms.locfileid: "52417798"
---
# <a name="explain-transact-sql"></a>EXPLAIN (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  返回 [!INCLUDE[ssDW](../../includes/ssdw-md.md)] [!INCLUDE[DWsql](../../includes/dwsql-md.md)] 语句的查询计划，但不运行该语句。 使用 EXPLAIN 预览需要数据移动的操作和查看查询操作的预计成本。  
  
 有关查询计划的详细信息，请参阅 [!INCLUDE[pdw-product-documentation_md](../../includes/pdw-product-documentation-md.md)] 中的“了解查询计划”。  
  
## <a name="syntax"></a>语法  
  

```  
EXPLAIN SQL_statement  
[;]  
```  
  
## <a name="arguments"></a>参数  
 SQL_statement  
 EXPLAIN 将在其上运行的 [!INCLUDE[DWsql](../../includes/dwsql-md.md)] 语句。 SQL_statement 可以是以下任一命令：SELECT、INSERT、UPDATE、DELETE、CREATE TABLE AS SELECT、CREATE REMOTE TABLE。  
  
## <a name="permissions"></a>Permissions  
 需要 SHOWPLAN 权限和执行 SQL_statement 的权限。 请参阅[权限：GRANT、DENY、REVOKE（Azure SQL 数据仓库、并行数据仓库）](../../t-sql/statements/permissions-grant-deny-revoke-azure-sql-data-warehouse-parallel-data-warehouse.md)。  
  
## <a name="return-value"></a>返回值  
 EXPLAIN 命令的返回值是 XML 文档，其结构如下所示。 此 XML 文档列出给定查询的查询计划中的所有操作，每个操作都由 `<dsql_operation>` 标记括起来。 返回值的类型为 nvarchar(max)。  
  
 返回的查询计划描述了 SQL 顺序语句；当查询运行时，它可能涉及并行操作，因此显示的一些顺序语句可以同时运行。  
  
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
  
|XML 标记|摘要、属性和内容|  
|-------------|--------------------------------------|  
|\<dsql_query>|顶级/文档元素。|
|\<sql>|回显 SQL_statement。|  
|\<params>|这次不使用此标记。|  
|\<dsql_operations>|总结和包含了查询步骤，以及查询的成本信息。 还包含所有 `<dsql_operation>` 块。 此标记包含整个查询的计数信息：<br /><br /> `<dsql_operations total_cost=total_cost total_number_operations=total_number_operations>`<br /><br /> total_cost 是要运行的查询的总预计时间（以毫秒为单位）。<br /><br /> total_number_operations 是查询的操作总数量。 并行和在多个节点上运行的操作将计为单个操作。|  
|\<dsql_operation>|描述查询计划中的单个操作。 \<dsql_operation> 将操作类型包含为属性：<br /><br /> `<dsql_operation operation_type=operation_type>`<br /><br /> operation_type 是[查询数据 (SQL Server PDW)](https://msdn.microsoft.com/3f4f5643-012a-4c36-b5ec-691c4bbe668c) 中说明的值之一。<br /><br /> `\<dsql_operation>` 块中的内容取决于操作类型。<br /><br /> 请参阅下表。|  
  
|操作类型|内容|示例|  
|--------------------|-------------|-------------|  
|BROADCAST_MOVE、DISTRIBUTE_REPLICATED_TABLE_MOVE、MASTER_TABLE_MOVE、PARTITION_MOVE、SHUFFLE_MOVE 和 TRIM_MOVE|具有这些属性的 `<operation_cost>` 元素。 值仅反映本地操作：<br /><br /> -   cost 是本地运算符成本，显示要运行的操作的预估时间（以毫秒为单位）。<br />-   accumulative_cost 是计划中看到的所有操作的总预估时间，包括并行操作的总值，以毫秒为单位。<br />-   average_rowsize 是操作期间行检索和传递的预估平均行大小（以字节为单位）。<br />-   output_rows 是输出（节点）基数，显示输出行数。<br /><br /> `<location>`：操作将在其中发生的节点或分发。 选项为：“Control”、“ComputeNode”、“AllComputeNodes”、“AllDistributions”、“SubsetDistributions”、“Distribution”和“SubsetNodes”。<br /><br /> `<source_statement>`：随机移动的源数据。<br /><br /> `<destination_table>`：数据将移至其中的内部临时表。<br /><br /> `<shuffle_columns>`：（仅适用于 SHUFFLE_MOVE 操作）。 将用作临时表分布列的一个或多个列。|`<operation_cost cost="40" accumulative_cost="40" average_rowsize = "50" output_rows="100"/>`<br /><br /> `<location distribution="AllDistributions" />`<br /><br /> `<source_statement type="statement">SELECT [TableAlias_3b77ee1d8ccf4a94ba644118b355db9d].[dist_date] FROM [qatest].[dbo].[flyers] [TableAlias_3b77ee1d8ccf4a94ba644118b355db9d]       </source_statement>`<br /><br /> `<destination_table>Q_[TEMP_ID_259]_[PARTITION_ID]</destination_table>`<br /><br /> `<shuffle_columns>dist_date;</shuffle_columns>`|  
|CopyOperation|`<operation_cost>`：请参阅上文的 `<operation_cost>`。<br /><br /> `<DestinationCatalog>`：一个或多个目标节点。<br /><br /> `<DestinationSchema>`：在 DestinationCatalog 中的目标架构。<br /><br /> `<DestinationTableName>`：目标表的名称或“TableName”。<br /><br /> `<DestinationDatasource>`：目标数据源的名称或连接信息。<br /><br /> `<Username>` 和 `<Password>`：这些字段表示可能需要目标用户名和密码。<br /><br /> `<BatchSize>`：复制操作 Batch 大小。<br /><br /> `<SelectStatement>`：用于执行复制的 select 语句。<br /><br /> `<distribution>`：在其中执行复制的分发。|`<operation_cost cost="0" accumulative_cost="0" average_rowsize="4" output_rows="1" />`<br /><br /> `<DestinationCatalog>master</DestinationCatalog>`<br /><br /> `<DestinationSchema>dbo</DestinationSchema>`<br /><br /> `<DestinationTableName>[TableName]</DestinationTableName>`<br /><br /> `<DestinationDatasource>localhost, 8080</DestinationDatasource>`<br /><br /> `<Username>...</Username>`<br /><br /> `<Password>...</Password>`<br /><br /> `<BatchSize>6000</BatchSize>`<br /><br /> `<SelectStatement>SELECT T1_1.c1 AS c1 FROM [qatest].[dbo].[gigs] AS T1_1</SelectStatement>`<br /><br /> `<distribution>ControlNode</distribution>`|  
|MetaDataCreate_Operation|`<source_table>`：用于操作的源表。<br /><br /> `<destionation_table>`：用于操作的目标表。|`<source_table>databases</source_table>`<br /><br /> `<destination_table>MetaDataCreateLandingTempTable</destination_table>`|  
|ON|`<location>`：请参阅上文的 `<location>`。<br /><br /> `<sql_operation>`：标识将在节点执行的 SQL 命令。|`<location permanent="false" distribution="AllDistributions">Compute</location>`<br /><br /> `<sql_operation type="statement">CREATE TABLE [tempdb].[dbo]. [Q_[TEMP_ID_259]]_ [PARTITION_ID]]]([dist_date] DATE) WITH (DISTRIBUTION = HASH([dist_date]),) </sql_operation>`|  
|RemoteOnOperation|`<DestinationCatalog>`：目标目录。<br /><br /> `<DestinationSchema>`：在 DestinationCatalog 中的目标架构。<br /><br /> `<DestinationTableName>`：目标表的名称或“TableName”。<br /><br /> `<DestinationDatasource>`：目标数据源的名称。<br /><br /> `<Username>` 和 `<Password>`：这些字段表示可能需要目标用户名和密码。<br /><br /> `<CreateStatement>`：目标数据库的表创建语句。|`<DestinationCatalog>master</DestinationCatalog>`<br /><br /> `<DestinationSchema>dbo</DestinationSchema>`<br /><br /> `<DestinationTableName>TableName</DestinationTableName>`<br /><br /> `<DestinationDatasource>DestDataSource</DestinationDatasource>`<br /><br /> `<Username>...</Username>`<br /><br /> `<Password>...</Password>`<br /><br /> `<CreateStatement>CREATE TABLE [master].[dbo].[TableName] ([col1] BIGINT) ON [PRIMARY] WITH(DATA_COMPRESSION=PAGE);</CreateStatement>`|  
|RETURN|`<resultset>`：结果集的标识符。|`<resultset>RS_19</resultset>`|  
|RND_ID|`<identifier>`：创建对象的标识符。|`<identifier>TEMP_ID_260</identifier>`|  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
 EXPLAIN 仅可应用于可优化的查询，即可基于 EXPLAIN 命令的结果改进或修改的查询。 上面列出了受支持的 EXPLAIN 命令。 尝试将 EXPLAIN 与不受支持的查询类型一起使用将返回错误或回显查询。  
  
 用户事务中不支持 EXPLAIN。  
  
## <a name="examples"></a>示例  
 以下示例展示了在 SELECT 语句中运行的 EXPLAIN 命令和 XML 结果。  
  
 **提交 EXPLAIN 语句**  
  
 此示例提交的命令是：  
  
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
  
 使用 EXPLAIN 选项执行语句后，消息选项卡显示标题为 explain ，并且以 XML 文本 `\<?xml version="1.0" encoding="utf-8"?>` 开头的单行。单击 XML 可在 XML 窗口打开完整的文本。 若要更好地了解以下注释，应启用 SSDT 中的行号显示。  
  
#### <a name="to-turn-on-line-numbers"></a>启用行号  
  
1.  输出显示在“解释”选项卡 SSDT 中，在“工具”菜单上，选择“选项”。  
  
2.  展开“文本编辑器”部分，展开“XML”，然后单击“常规”。  
  
3.  在“显示”区域中，检查“行号”。  
  
4.  单击“确定” 。  
  
 **EXPLAIN 输出示例**  
  
 启用了行号的 EXPLAIN 命令的 XML 结果为：  
  
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
  
 **EXPLAIN 输出的含义**  
  
 上面的输出包含 144 行带编号的行。 此查询的输出可能略有不同。 以下列表显示了重要部分。  
  
-   第 3 行到第 16 行提供了正在分析的查询的描述。  
  
-   第 17 行指定操作的总数将为 9。 可以通过查找单词 dsql_operation 来查找每个操作的开始部分。  
  
-   第 18 行开始操作 1。 第 18 行和第 19 行表示 RND_ID 操作将创建一个用于对象描述的随机 ID 号。 上面的输出中所述的对象是 TEMP_ID_16893。 你的编号会不同。  
  
-   第 20 行开始操作 2。 第 21 行至第 25 行：在所有计算节点上，创建一个名为 TEMP_ID_16893 的临时表。  
  
-   第 26 行开始操作 3。 第 27 行至第 37 行：通过使用广播将数据移动到 TEMP_ID_16893。 提供发送给每个计算节点的查询。 第 37 行指定目标表为 TEMP_ID_16893。  
  
-   第 38 行开始操作 4。 第 39 行至第 40 行：创建表的随机 ID。 TEMP_ID_16894 是在上面的示例的 ID 编号。 你的编号会不同。  
  
-   第 41 行开始操作 5。 第 42 行至第 46 行：在所有节点上，创建一个名为 TEMP_ID_16894 的临时表。  
  
-   第 47 行开始操作 6。 第 48 行至第 91 行：通过使用随机移动操作，将数据从各种表（包括 TEMP_ID_16893）移到表 TEMP_ID_16894。 提供发送给每个计算节点的查询。 第 90 行指定目标表为 TEMP_ID_16894。 第 91 行指定列。  
  
-   第 92 行开始操作 7。 第 93 行至第 97 行：在所有计算节点上，删除临时表 TEMP_ID_16893。  
  
-   第 98 行开始操作 8。 第 99 行至第 135 行：将结果返回到客户端。 使用提供的查询来获取结果。  
  
-   第 136 行开始操作 9。 第 137 行至第 140 行：在所有节点上，删除临时表 TEMP_ID_16894。  
  
  

