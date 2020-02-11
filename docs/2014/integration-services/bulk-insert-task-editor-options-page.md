---
title: 大容量插入任务编辑器（"选项" 页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.bulkinserttask.options.f1
helpviewer_keywords:
- Bulk Insert Task Editor
ms.assetid: b3702811-3eb8-4b28-9190-5ae7a1a7bb6f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e7cb19e3ba2f58a39ffd87bdabc6eb1ad18a1d18
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66061193"
---
# <a name="bulk-insert-task-editor-options-page"></a>大容量插入任务编辑器（“选项”页）
  使用 **“大容量插入任务编辑器”** 对话框的 **“选项”** 页，可以设置大容量插入操作的属性。 大容量插入任务将大量数据复制到[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]表或视图中。  
  
 若要了解如何使用大容量插入，请参阅[大容量插入任务](control-flow/bulk-insert-task.md)和 [BULK INSERT (Transact-SQL)](/sql/t-sql/statements/bulk-insert-transact-sql)。  
  
## <a name="options"></a>选项  
 **CodePage**  
 指定数据文件中数据的代码页。  
  
 **DataFileType**  
 指定在加载操作中要使用的数据类型值。  
  
 **BatchSize**  
 指定每批中的行数。 默认设置为整个数据文件。 如果将 **BatchSize** 设置为零，则数据是在一批中加载的。  
  
 **LastRow**  
 指定要复制的最后一行。  
  
 **FirstRow**  
 指定要开始复制的第一行。  
  
 **选项**  
 |术语|定义|  
|----------|----------------|  
|**检查约束**|选择此项将检查表约束和列约束。|  
|**保留 Null**|选择此项将在大容量插入操作期间保留 Null 值，而不是为空列插入任意默认值。|  
|**启用标识插入**|选择此项可将现有值插入到标识列中。|  
|**表锁**|选择此项将在大容量插入期间锁定表。|  
|**激发触发器**|选择此项将激发对表上的触发器的任意插入、更新或删除操作。|  
  
 **SortedData**  
 指定大容量插入语句中的 ORDER BY 子句。 所提供的列名必须是目标表中的有效列。 默认为 `false`。 这意味着 ORDER BY 子句将不对数据进行排序。  
  
 **MaxErrors**  
 指定在取消大容量插入操作之前可以发生的最大错误数量。 如果值为 0，则指示对错误的数量没有限制。  
  
> [!NOTE]  
>  大容量加载操作不能导入的每一行都被计为一个错误。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [大容量插入任务编辑器 &#40;常规页&#41;](general-page-of-integration-services-designers-options.md)   
 [大容量插入任务编辑器 &#40;连接页&#41;](../../2014/integration-services/bulk-insert-task-editor-connection-page.md)   
 [“表达式”页](expressions/expressions-page.md)   
 [控制流](control-flow/control-flow.md)  
  
  
