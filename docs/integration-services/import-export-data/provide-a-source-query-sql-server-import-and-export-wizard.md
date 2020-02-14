---
title: 提供源查询（SQL Server 导入和导出向导）| Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.providesourcequery.f1
ms.assetid: c8cbd07e-b9c3-422f-94b8-d6fc8cf31cf5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 095852eb02ba78c261b19a0a96fb639075ee5eab
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "71285127"
---
# <a name="provide-a-source-query-sql-server-import-and-export-wizard"></a>提供源查询（SQL Server 导入和导出向导）

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


如果指定要提供查询以选择要复制的数据，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导会显示“提供源查询”  。 在此页上，可编写并测试选择要从数据源复制到目标的数据的 SQL 查询。 还可以粘贴已保存的查询的文本或从文件加载它。

## <a name="screen-shot-of-the-source-query-page"></a>“源查询”页的屏幕截图  
以下屏幕截图显示向导的“提供源查询”  页。
 
在此简单示例中，用户输入了查询 `SELECT * FROM Sales.Customer`，用于从源数据库中的 Sales.Customer 表复制所有行和所有列  。
-   `SELECT *` 表示复制所有列。
-   缺少 `WHERE` 子句表示复制所有行。
  
 ![“导入和导出向导”的“源查询”页面](../../integration-services/import-export-data/media/source-query.png "“导入和导出向导”的“源查询”页面")  

## <a name="provide-the-query-and-check-its-syntax"></a>提供查询，并检查其语法
**SQL 语句**  
 输入 SELECT 查询，以便从源数据库中检索特定数据行和数据列。 还可以粘贴已保存查询的文本，或通过单击“浏览”从文件加载它  。 
  
 例如，以下查询可以从 AdventureWorks 示例数据库中检索提成比例超过 1.5% 的销售人员的 SalesPersonID、SalesQuota 和 SalesYTD    。  
  
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
 使用“打开”对话框选择包含 SQL 查询的文本的已保存文件  。 选择一个文件可以将该文件中的文本复制到“SQL 语句”  文本框中。  
 
## <a name="excelQueries"></a> 为 Excel 提供源查询

> [!IMPORTANT]
> 有关连接到 Excel 文件的详细信息，以及从 Excel 文件加载数据或将数据加载到 Excel 文件的限制和已知问题，请参阅[使用 SQL Server Integration Services (SSIS) 从 Excel 加载数据或将数据加载到 Excel 中](../load-data-to-from-excel-with-ssis.md)。

可查询三种类型的 Excel 对象。
-   **工作表。** 若要查询工作表，请将 $ 字符附加到表名称的末尾，并用分隔符包含字符串 - 例如， **[Sheet1$]** 。

    ```sql
    SELECT * FROM [Sheet1$]
    ```

-   **命名区域。** 若要查询命名区域，只需使用区域名称 - 例如， **MyDataRange**。
    
    ```sql
    SELECT * FROM MyDataRange
    ```

-   **未命名区域。** 若要指定未命名的单元格区域，请将 $ 字符附加到表名称的末尾，添加区域说明，并用分隔符包围字符串 - 例如， **[Sheet1$ A1: B4]** 。

    ```sql
    SELECT * FROM [Sheet1$A1:B4]
    ```

## <a name="whats-next"></a>下一步是什么？  
 编写并测试选择要从复制的数据的 SQL 查询之后，下一页取决于数据目标。  
  
-   对于大多数目标，下一页是“选择源表和源视图”  。 在此页上，可查看提供的查询以及（可选）选择要复制的列和预览示例数据。 有关详细信息，请参阅 [选择源表和源视图](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md)。  
  
-   如果目标是平面文件，则下一页是“配置平面文件目标”  。 在此页上，可为目标平面文件指定格式设置选项。 （配置平面文件之后，随后下一页是“选择源表和源视图”  。）有关详细信息，请参阅[配置平面文件目标](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md)。  


