---
title: SQL Server 目标自定义属性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: b736aa6d-c154-44a0-be08-f25733fca1d9
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 073026ea048f545d404c0b656b721fb72ed7cc8e
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84914065"
---
# <a name="sql-server-destination-custom-properties"></a>SQL Server 目标自定义属性
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目标具有自定义属性和所有数据流组件共有的属性。  
  
 下表介绍了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目标的自定义属性。 所有属性均可读/写。  
  
|属性名称|数据类型|说明|  
|-------------------|---------------|-----------------|  
|AlwaysUseDefaultCodePage|Boolean|强制使用 DefaultCodePage 属性值。 此属性的默认值为 `False`。|  
|BulkInsertCheckConstraints|Boolean|一个值，指定大容量插入是否检查约束。 此属性的默认值为 `True`。|  
|BulkInsertFireTriggers|Boolean|一个值，指定大容量插入是否对表激发触发器。 此属性的默认值为 `False`。|  
|BulkInsertFirstRow|Integer|一个值，指定要插入的第一行。 此属性的默认值为 **-1**，表示尚未分配值|  
|BulkInsertKeepIdentity|Boolean|一个值，指定值是否可以插入到标识列。 此属性的默认值为 `False`。|  
|BulkInsertKeepNulls|Boolean|一个值，指定大容量插入是否可以保持 Null 值。 此属性的默认值为 `False`。|  
|BulkInsertLastRow|Integer|一个值，指定要插入的最后一行。 此属性的默认值为 **-1**，表示尚未分配值。|  
|BulkInsertMaxErrors|Integer|一个值，指定在大容量插入任务停止之前可以发生的错误数。 此属性的默认值为 **-1**，表示尚未分配值。|  
|BulkInsertOrder|String|排序列的名称。 每一列都可以按升序或降序排序。 如果使用了多个排序列，则使用逗号分隔列名称。|  
|BulkInsertTableName|String|向其中复制数据的数据库中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表或视图。|  
|BulkInsertTablock|Boolean|一个值，指定大容量插入期间是否锁定表。 此属性的默认值为 `True`。|  
|DefaultCodePage|Integer|当数据源中的代码页信息不可用时要使用的代码页。|  
|MaxInsertCommitSize|Integer|一个值，指定一批可以插入的最大行数。 当值为零时，可一批插入所有的行。|  
|超时|Integer|一个值，指定如果没有数据需要插入， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目标终止前等待的秒数。 值 0 表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目标将不会超时。此属性的默认值为 30。|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目标的输入和输入列没有自定义属性。  
  
 有关详细信息，请参阅 [SQL Server Destination](sql-server-destination.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Common Properties](../common-properties.md)  
  
  
