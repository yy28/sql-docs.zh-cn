---
title: "SQL 目标编辑器 （高级页） |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.sqlserverdestadapter.advanced.f1
helpviewer_keywords:
- SQL Server Destination Editor
ms.assetid: 9b46bcf8-ddaf-4d7d-90a6-80bc19517e9b
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e279b5bc6ff340323647d1a93daeb006ec4c3cbf
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="sql-destination-editor-advanced-page"></a>SQL 目标编辑器（“高级”页）
  可以使用 **“SQL 目标编辑器”** 对话框的 **“高级”** 页指定大容量插入高级选项。  
  
 若要了解有关 SQL Server 目标的详细信息，请参阅 [SQL Server Destination](../../integration-services/data-flow/sql-server-destination.md)。  
  
## <a name="options"></a>选项  
 **保留标识**  
 指定任务是否应在标识列中插入值。 此属性的默认值为 **False**。  
  
 **保留 Null**  
 指定任务是否应保留空值。 此属性的默认值为 **False**。  
  
 **表锁**  
 指定在加载数据时是否锁定表。 此属性的默认值为 **True**。  
  
 **检查约束**  
 指定任务是否应检查约束。 此属性的默认值为 **True**。  
  
 **激发触发器**  
 指定大容量插入任务是否应对表激发触发器。 此属性的默认值为 **False**。  
  
 **首行**  
 指定要插入的第一行。 此属性的默认值为 **-1**，表示尚未分配值。  
  
> [!NOTE]  
>  如果在 **“SQL 目标编辑器”** 中清空此文本框，则表示不希望为此属性分配值。 请在“属性”窗口、“高级编辑器”和对象模型中使用 -1。  
  
 **末行**  
 指定要插入的最后一行。 此属性的默认值为 **-1**，表示尚未分配值。  
  
> [!NOTE]  
>  如果在 **“SQL 目标编辑器”** 中清空此文本框，则表示不希望为此属性分配值。 请在“属性”窗口、“高级编辑器”和对象模型中使用 -1。  
  
 **最大错误数**  
 指定在大容量插入任务停止之前可以发生的错误数量。 此属性的默认值为 **–1**，表示尚未分配值。  
  
> [!NOTE]  
>  如果在 **“SQL 目标编辑器”** 中清空此文本框，则表示不希望为此属性分配值。 请在“属性”窗口、“高级编辑器”和对象模型中使用 -1。  
  
 **超时**  
 指定在大容量插入任务因超时而停止之前等待的秒数。  
  
 **设置列顺序**  
 键入排序列的名称。 每一列都可以按升序或降序排序。 如果您使用多个排序列，请用逗号分隔列表。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../integration-services/integration-services-error-and-message-reference.md)   
 [SQL 目标编辑器 &#40;连接管理器页 &#41;](../../integration-services/data-flow/sql-destination-editor-connection-manager-page.md)   
 [SQL 目标编辑器 &#40;映射页 &#41;](../../integration-services/data-flow/sql-destination-editor-mappings-page.md)   
 [通过使用 SQL Server 目标大容量加载数据](../../integration-services/data-flow/bulk-load-data-by-using-the-sql-server-destination.md)  
  
  
