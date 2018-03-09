---
title: "提供源查询（SQL Server 导入和导出向导）| Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.providesourcequery.f1
ms.assetid: c8cbd07e-b9c3-422f-94b8-d6fc8cf31cf5
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 4399fdeb68ee0768ac083e0193ae0513b221021d
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="provide-a-source-query-sql-server-import-and-export-wizard"></a>提供源查询（SQL Server 导入和导出向导）
如果指定要提供查询以选择要复制的数据，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导会显示“提供源查询” 。 在此页上，可编写并测试选择要从数据源复制到目标的数据的 SQL 查询。 还可以粘贴已保存的查询的文本或从文件加载它。

## <a name="screen-shot-of-the-source-query-page"></a>“源查询”页的屏幕截图  
以下屏幕截图显示向导的“提供源查询”  页。
 
在此简单示例中，用户输入了查询 `SELECT * FROM Sales.Customer`，用于从源数据库中的 Sales.Customer 表复制所有行和所有列。
-   `SELECT *` 表示复制所有列。
-   缺少 `WHERE` 子句表示复制所有行。
  
 ![导入和导出向导的“源查询”页](../../integration-services/import-export-data/media/source-query.png "Source query page of the Import and Export Wizard")  

## <a name="provide-the-query-and-check-its-syntax"></a>提供查询，并检查其语法
**SQL 语句**  
 输入 SELECT 查询，以便从源数据库中检索特定数据行和数据列。 还可以粘贴已保存查询的文本，或通过单击“浏览”从文件加载它。 
  
 例如，以下查询可以从 AdventureWorks 示例数据库中检索提成比例超过 1.5% 的销售人员的 SalesPersonID、SalesQuota 和 SalesYTD。  
  
```sql
SELECT SalesPersonID, SalesQuota, SalesYTD  
FROM Sales.SalesPerson  
WHERE CommissionPct > 0.015  
```  

有关 SELECT 查询的更多示例，请参阅 [SELECT 示例 (Transact-SQL)](../../t-sql/queries/select-examples-transact-sql.md) 或联机搜索。  

如果数据源是 Excel，请参阅本主题后的 [为 Excel 提供源查询](#excelQueries) ，以便了解如何在查询中指定 Excel 工作表和区域。
  
 **分析**  
 检查在“SQL 语句”  文本框中输入的 SQL 语句的语法。  
  
> [!NOTE]
> 如果检查语句的语法所需的时间超过超时值（30 秒），则将停止分析并引发错误。 在成功完成分析之前，无法跳过向导的这一页。 避免超时的一种解决方案是基于要使用的查询创建数据库视图，然后从向导查询该视图，而不是直接输入查询文本。  
  
 **“浏览”**  
 使用“打开”对话框选择包含 SQL 查询的文本的已保存文件。 选择一个文件可以将该文件中的文本复制到“SQL 语句”  文本框中。  
 
## <a name="excelQueries"></a> 为 Excel 提供源查询
### <a name="specify-excel-objects-in-queries"></a>在查询中指定 Excel 对象
可查询三种类型的 Excel 对象。
-   **工作表。** 若要查询工作表，请将 $ 字符附加到表名称的末尾，并用分隔符包含字符串 - 例如， **[Sheet1$]**。

    ```sql
    SELECT * FROM [Sheet1$]
    ```

-   **命名区域。** 若要查询命名区域，只需使用区域名称 - 例如， **MyDataRange**。
    
    ```sql
    SELECT * FROM MyDataRange
    ```

-   **未命名区域。** 若要指定未命名的单元格区域，请将 $ 字符附加到表名称的末尾，添加区域说明，并用分隔符包围字符串 - 例如， **[Sheet1$ A1: B4]**。

    ```sql
    SELECT * FROM [Sheet1$A1:B4]
    ```

### <a name="prepare-the-excel-source-data"></a>准备 Excel 源数据
无论是否将工作表或区域指定为源表，该驱动程序都将读取从工作表或区域左上角第一个非空单元开始的连续  单元块。 因此，源数据中不能有空行。 例如，列标题和数据行之间不能有空行。 如果工作表顶部数据上面的标题后跟有空行，则无法查询该工作表。 在 Excel 中，必须为区域内的数据分配名称，并查询命名区域而非工作表。

## <a name="whats-next"></a>下一步是什么？  
 编写并测试选择要从复制的数据的 SQL 查询之后，下一页取决于数据目标。  
  
-   对于大多数目标，下一页是“选择源表和源视图” 。 在此页上，可查看提供的查询以及（可选）选择要复制的列和预览示例数据。 有关详细信息，请参阅 [选择源表和源视图](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md)。  
  
-   如果目标是平面文件，则下一页是“配置平面文件目标” 。 在此页上，可为目标平面文件指定格式设置选项。 （配置平面文件之后，随后下一页是“选择源表和源视图”。）有关详细信息，请参阅[配置平面文件目标](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md)。  


