---
title: “全文索引”对话框 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.fulltextindex
ms.assetid: ef45b585-2567-4abe-b421-9fd0994e0146
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: adb00f8b0e7cb009420e9843532c3f3d4deb0833
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63028404"
---
# <a name="full-text-index-dialog-box-visual-database-tools"></a>“全文索引”对话框 (Visual Database Tools)
  使用此对话框可以创建全文索引，用于对数据库表中基于文本的列进行全文搜索。 全文索引依赖于常规索引，因此必须先创建常规索引。 常规索引只能对单个非空的列创建，而且最好选择值较小的列而不是选择值较大的列。  
  
> [!NOTE]  
>  若要创建全文索引，必须先使用外部工具（如 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或企业管理器）为数据库创建一个全文本目录。  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的每个版本中都不提供全文检索功能。 有关各个版本支持的功能列表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，请参阅 SQL Server 2014 的各个[版本支持的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
## <a name="options"></a>选项  
 **选定的全文索引**  
 列出现有的全文索引。 选择一个索引即可在右侧的网格中显示其属性。 如果该列表为空，则表示尚未为该表定义任何全文本关系。  
  
 **添加**  
 创建新的全文索引。  
  
 **删除**  
 删除在“选定的全文检索”  列表中所选的全文检索。  
  
 **常规类别**  
 展开此项可显示“列”  和“全文本目录名称”  。  
  
 **“列”**  
 显示一个逗号分隔列表，其中列出了可进行全文搜索的列的名称。 若要查看完整列表，请单击该属性字段左侧的省略号按钮“(…)”  。  
  
 **全文本目录名称**  
 显示用于存储此全文索引的全文本目录的名称。 若要将索引存储在其他目录中，请单击当前目录名称，再从下拉列表中选择其他目录。  
  
> [!NOTE]  
>  必须先在外部工具（例如 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或企业管理器）中创建目录。  
  
 **标识类别**  
 展开此项可显示此索引的名称字段。  
  
 **名称**  
 显示此全文索引的系统指定名称。  
  
 **表设计器类别**  
 展开此项可显示指示索引执行方式的属性。  
  
 **活动**  
 显示当前是否可以使用此全文索引执行全文搜索。  
  
 **更改跟踪设置**  
 描述此索引的更改跟踪状态：“手动”、“自动”或“关闭”。  
  
 **爬网已完成**  
 显示最近一次爬网是否已完成。 如果此属性值为“否”，则表示爬网当前正在进行。  
  
 **当前或上一次爬网的结束日期和时间**  
 显示最近一次爬网的结束日期和时间。  
  
 **当前或上一次爬网中的错误数**  
 显示当前或最近一次爬网中的错误数。  
  
 **索引版本**  
 显示爬网开始时表的架构版本。  
  
 **当前或上一次爬网中的行数**  
 显示在当前或最近一次爬网中更新的行数。  
  
 **当前或上一次爬网的开始日期和时间**  
 显示当前或最近一次爬网的开始日期和时间。  
  
 **下一次爬网的时间戳**  
 显示下一次爬网的开始日期和时间。  
  
 **当前或上一次爬网的类型**  
 显示当前或最近一次爬网的类型：“完全”、“增量”、“更新”或“自动传播”。  
  
 **唯一索引名称**  
 显示此数据库中具有唯一单列索引的所有列的名称列表。 这些列可用于创建全文索引。  
  
## <a name="see-also"></a>另请参阅  
 [使用全文索引向导](../../relational-databases/search/use-the-full-text-indexing-wizard.md)   
 [CREATE FULLTEXT INDEX (Transact-SQL)](/sql/t-sql/statements/create-fulltext-index-transact-sql)  
  
  
