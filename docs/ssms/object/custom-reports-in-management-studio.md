---
title: "Management Studio 中的自定义报表 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.summary.new.custom.report.f1
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], custom reports
ms.assetid: 1ba3f758-f39b-4f5f-91ca-516cedc78979
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b1292293885329df9b38dfcf94cd8ee1c5ca5238
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="custom-reports-in-management-studio"></a>Management Studio 中的自定义报表
在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 中，很多对象资源管理器节点都显示一组由 [!INCLUDE[msCoName](../../includes/msconame_md.md)] 创建的标准报表。 这些报表汇总了通常请求的服务器信息。 从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] Service Pack 2 开始，管理员可以从 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull_md.md)] 中运行使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)]创建的自定义报表。  
  
## <a name="implementation"></a>实现  
自定义报表是使用报表定义语言 (RDL) 创建的，并存储为报表定义 (.rdl) 文件。 RDL 包含 XML 格式的报表的数据检索和布局信息。 RDL 是一个开放式架构。 开发人员可以使用其他属性和元素来扩展 RDL。 报表可以执行位于报表内部的任何有效的 [!INCLUDE[tsql](../../includes/tsql_md.md)] 语句。  
  
如果将对象资源管理器连接至服务器，并且自定义报表引用了当前所选对象资源管理器节点的报表参数，则该自定义报表可在此节点的上下文中执行。 这样，报表可以使用当前上下文（如当前数据库）或统一的上下文（如在自定义报表包含的 [!INCLUDE[tsql](../../includes/tsql_md.md)] 语句中指定一个专门数据库）。  
  
## <a name="running-a-custom-report"></a>运行自定义报表  
可以在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] 中通过以下方式运行自定义报表：  
  
-   在对象资源管理器中，右键单击一个节点，指向“报表”，再左键单击“自定义报表”。 在“打开文件”对话框中，找到包含 .rdl 文件的文件夹，然后打开相应的报表文件。  
  
-   在对象资源管理器中，右键单击一个节点，指向“报表”，再指向“自定义报表”，然后从最近打开的文件列表中选择一个自定义报表。  
  
## <a name="limitations"></a>限制  
在使用自定义报表时，请注意以下限制：  
  
-   若要防止意外执行恶意代码，即使配置了文件系统以将 .rdl 文件与 [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] 相关联，也不能将 [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)]配置为自动运行报表。 不能在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] 中以编程方式执行报表，也不能通过 [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)]从命令行中运行报表。  
  
-   可以在没有生成预期值的上下文中运行自定义报表。 例如，可以在复制未涉及的数据库的上下文中运行有关复制的报表，也可以作为无权访问生成准确报表所需信息的用户运行报表。 自定义报表的创建者负责验证报表结构及其上下文。  
  
-   不能将自定义报表添加到标准报表列表中。  
  
-   由报表处理的代码可能会影响服务器性能。  
  
-   自定义报表不支持子报表。  
  
-   不得通过表达式定义报表中每个查询的命令文本。  
  
-   命令（查询）中使用的任何查询参数都只能引用单个报表参数，而不能使用任何表达式运算符。  
  
-   报表命令（查询）只支持“文本”和“存储过程”命令类型。  
  
-   报表框架不为查询提供任何参数转义。 查询的创建者必须确保他们的查询不会受到 SQL 注入攻击。  
  
## <a name="managing-custom-reports"></a>管理自定义报表  
如果用户具有很多自定义报表，建议他们使用具有相应 NTFS 文件系统权限的文件系统文件夹来组织这些报表。  
  
## <a name="permissions"></a>Permissions  
自定义报表是使用当前用户的权限运行的。 若要防止恶意用户更改报表运行的查询，应将包含报表文件的文件系统文件夹的权限设置为“限制访问”。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 服务所使用的用户和帐户都要求对包含报表文件的文件系统文件夹具有读取权限。  
  
可以在报表中嵌入任何有效的 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 命令，但不会执行该命令。  
  
> [!CAUTION]  
> 可以在报表中嵌入任何有效的 [!INCLUDE[tsql](../../includes/tsql_md.md)] 语句，并可从报表执行此语句。 如果使用具有较高特权的用户帐户运行报表，则可以不受约束地执行所有这些嵌入的指令。  
  

  
## <a name="see-also"></a>另请参阅  
[向 Management Studio 添加自定义报表](../../ssms/object/add-a-custom-report-to-management-studio.md)  
[启用运行自定义报表警告](../../ssms/object/unsuppress-run-custom-report-warnings.md)  
[将自定义报表与对象资源管理器节点属性一起使用](../../ssms/object/use-custom-reports-with-object-explorer-node-properties.md)  
  

