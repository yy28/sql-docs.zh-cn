---
title: CDC 源 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.cdcsource.f1
ms.assetid: 99775608-e177-44ed-bb44-aaccb0f4f327
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 80e557d9d286040b1d145c852779a9eca5cd4e64
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58382723"
---
# <a name="cdc-source"></a>CDC 源
  CDC 源从 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更改表中读取某一范围的更改数据并且将更改向下传递给其他 SSIS 组件。  
  
 由 CDC 源读取的更改数据的范围称作 CDC 处理范围并且由在当前数据流开始前执行的 CDC 控制任务确定。 该 CDC 处理范围是从维护一组表的 CDC 处理状态的包变量的值派生的。  
  
 CDC 源通过使用数据库表、视图或 SQL 语句，从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中提取数据。  
  
 CDC 源使用以下配置：  
  
-   用于访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC 数据库的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ADO.NET 连接管理器。 有关配置 CDC 源连接的详细信息，请参阅 [CDC 源编辑器（“连接管理器”页）](../cdc-source-editor-connection-manager-page.md)。  
  
-   为 CDC 启用的表。  
  
-   所选表（如果存在多个）的捕获实例的名称。  
  
-   更改处理模式。  
  
-   基于所确定的 CDC 处理范围的 CDC 状态包变量的名称。 CDC 源不修改该变量。  
  
 CDC 源返回的数据与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC 函数 cdc.fn_cdc_get_all_changes_\<capture-instance-name> 或 cdc.fn_cdc_get_net_changes_\<capture-instance-name>（在可用时）返回的数据相同。 唯一可选的添加是列 **__$initial_processing** ，它指示当前处理范围是否可与表的初始加载重叠。 有关初始处理的详细信息，请参阅 [CDC Control Task](../control-flow/cdc-control-task.md)。  
  
 CDC 源有一个常规输出和一个错误输出。  
  
## <a name="error-handling"></a>错误处理  
 CDC 源有一个错误输出。 组件的错误输出包括以下输出列：  
  
-   **错误代码**:值始终为-1。  
  
-   **错误列**:导致错误 （针对转换错误） 的源列。  
  
-   **错误行列**:导致错误的记录数据。  
  
 根据错误行为设置，CDC 源支持在错误输出中返回在提取过程中发生的错误（数据转换、截断）。 有关详细信息，请参阅 [CDC 源编辑器（“错误输出”页）](../cdc-source-editor-error-output-page.md)。  
  
## <a name="data-type-support"></a>数据类型支持  
 Microsoft 的 CDC 源组件支持所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型，这些数据类型映射到正确的 SSIS 数据类型。  
  
## <a name="troubleshooting-the-cdc-source"></a>CDC 源故障排除  
 下面包含与排除 CDC 源问题有关的信息。  
  
### <a name="use-this-script-to-isolate-problems-and-reproduce-them-in-sql-server-management-studio"></a>使用此脚本可以确定问题并且在 SQL Server Management Studio 中复现这些问题  
 CDC 源操作受到在调用 CDC 源之前执行的 CDC 控制任务操作的约束。 CDC 控制任务准备 CDC 状态包变量的值以便包含开始和结束 LSN。 它执行与下面的脚本等效的函数：  
  
```  
use <cdc-enabled-database-name>  
               declare @start_lsn binary(10), @end_lsn binary(10)  
               set @start_lsn = sys.fn_cdc_increment_lsn(  
                       convert(binary(10),'0x' + '<value-from-state-cs>', 1))  
               set @end_lsn =   
                       convert(binary(10),'0x' + '<value-from-state-ce>', 1)  
               select * from cdc.fn_cdc_get_net_changes_dbo_Table1(@start_lsn,  
@end_lsn, '<mode>')  
```  
  
 其中：  
  
-   \<cdc-enabled-database-name> 是包含更改表的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的名称。  
  
-   \<value-from-state-cs> 是在 CDC 状态变量中以 CS/\<value-from-state-cs>/（CS 表示 Current-processing-range-Start）形式出现的值。  
  
-   \<value-from-state-ce> 是在 CDC 状态变量中以 CE/\<value-from-state-cs>/（CE 表示 Current-processing-range-End）形式出现的值。  
  
-   \<mode> 是 CDC 处理模式。 处理模式具有以下值之一： **“全部”**、 **“全部且具有旧值”**、 **“净值”**、 **“具有更新掩码的净值”** 和 **“净值且具有合并”**。  
  
 此脚本可通过在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中复现问题（在其中可以轻松地复现和标识错误），有助于标识问题。  
  
#### <a name="sql-server-error-message"></a>SQL Server 错误消息  
 下面是可以由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回的消息：  
  
 为过程或函数 cdc.fn_cdc_get_net_changes_\<..> 提供的参数数目不足。  
  
 此错误并不表示缺少参数。 这意味着 CDC 状态变量中的开始或结束 LSN 值无效。  
  
## <a name="configuring-the-cdc-source"></a>配置 CDC 源  
 您可以通过编程方式或者通过 SSIS 设计器配置 CDC 源。  
  
 有关详细信息，请参阅下列主题之一：  
  
-   [CDC 源编辑器（“连接管理器”页）](../cdc-source-editor-connection-manager-page.md)  
  
-   [CDC 源编辑器（“列”页）](../cdc-source-editor-columns-page.md)  
  
-   [CDC 源编辑器（“错误输出”页）](../cdc-source-editor-error-output-page.md)  
  
 **“高级编辑器”** 对话框包含可通过编程方式设置的属性。  
  
 打开 **“高级编辑器”** 对话框：  
  
-   在您的 **项目的** “数据流” [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 屏幕上，右键单击 CDC 源，然后选择 **“显示高级编辑器”**。  
  
 有关可在 **“高级编辑器”** 对话框中设置的属性的详细信息，请参阅 [CDC Source Custom Properties](cdc-source-custom-properties.md)。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [CDC 源编辑器（“连接管理器”页）](../cdc-source-editor-connection-manager-page.md)  
  
-   [CDC 源编辑器（“列”页）](../cdc-source-editor-columns-page.md)  
  
-   [CDC 源编辑器（“错误输出”页）](../cdc-source-editor-error-output-page.md)  
  
-   [CDC Source Custom Properties](cdc-source-custom-properties.md)  
  
-   [使用 CDC 源提取更改数据](cdc-source.md)  
  
## <a name="related-content"></a>相关内容  
  
-   mattmasson.com 上的博客文章 [CDC 源的处理模式](https://go.microsoft.com/fwlink/?LinkId=242541)。  
  
  
