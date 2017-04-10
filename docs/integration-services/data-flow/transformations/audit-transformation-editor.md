---
title: "审核转换编辑器 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.audittransformation.f1"
helpviewer_keywords: 
  - "审核转换编辑器"
ms.assetid: 32786a34-5870-4fde-83c7-ec74d62404b8
caps.latest.revision: 13
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 13
---
# 审核转换编辑器
  通过进行审核转换，包中的数据流可以包含有关运行包的环境的数据。 例如，包、计算机和操作员的名称可添加到数据流中。 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中包含了提供这些信息的系统变量。  
  
 若要了解有关审核转换的详细信息，请参阅 [Audit Transformation](../../../integration-services/data-flow/transformations/audit-transformation.md)。  
  
## 选项  
 **输出列的名称**  
 为包含审核信息的新输出列提供名称。  
  
 **审核类型**  
 选择用于提供审核信息的可用系统变量。  
  
|“值”|Description|  
|-----------|-----------------|  
|**执行实例 GUID**|插入唯一标识包的执行实例的 GUID。|  
|**包 ID**|插入唯一标识包的 GUID。|  
|**包名称**|插入包名称。|  
|**版本 ID**|插入唯一标识包版本的 GUID。|  
|**执行开始时间**|插入包执行的开始时间。|  
|**计算机名称**|插入启动包的计算机的名称。|  
|**用户名**|插入启动包的用户的登录名。|  
|**任务名称**|插入与审核转换相关联的数据流任务的名称。|  
|**任务 ID**|插入唯一标识与审核转换相关联的数据流任务的 GUID。|  
  
## 另请参阅  
 [Integration Services 错误和消息引用](../../../integration-services/integration-services-error-and-message-reference.md)  
  
  