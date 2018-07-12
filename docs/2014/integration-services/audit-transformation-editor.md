---
title: 审核转换编辑器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.audittransformation.f1
helpviewer_keywords:
- Audit Transformation Editor
ms.assetid: 32786a34-5870-4fde-83c7-ec74d62404b8
caps.latest.revision: 12
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f0ec690b0c1b90ffc01c5bf275769658c72ffc99
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37148348"
---
# <a name="audit-transformation-editor"></a>审核转换编辑器
  通过进行审核转换，包中的数据流可以包含有关运行包的环境的数据。 例如，包、计算机和操作员的名称可添加到数据流中。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中包含了提供这些信息的系统变量。  
  
 若要了解有关审核转换的详细信息，请参阅 [Audit Transformation](data-flow/transformations/audit-transformation.md)。  
  
## <a name="options"></a>“常规”  
 **输出列的名称**  
 为包含审核信息的新输出列提供名称。  
  
 **审核类型**  
 选择用于提供审核信息的可用系统变量。  
  
|ReplTest1|Description|  
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
  
## <a name="see-also"></a>请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  
