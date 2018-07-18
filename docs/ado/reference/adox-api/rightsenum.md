---
title: RightsEnum |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RightsEnum
helpviewer_keywords:
- RightsEnum enumeration [ADOX]
ms.assetid: 55ee67c7-a583-42aa-849a-78264b4cb614
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 32cd777bad44e0784943aab1c0a4c9ba665f7247
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35286846"
---
# <a name="rightsenum"></a>RightsEnum
指定对某个对象的权限或组或用户的权限。  
  
|常量|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**adRightCreate**|16384 (&AMP; H4000)|用户或组有权创建此类型的新对象。|  
|**adRightDelete**|65536 (&AMP; H10000)|用户或组有权从对象中删除数据。 如对象**表**，用户有权从记录中删除数据值。|  
|**adRightDrop**|256 (&AMP; H100)|用户或组有权从目录中删除对象。 例如，**表**可以通过删除表 SQL 命令来删除。|  
|**adRightExclusive**|512 (&AMP; H200)|用户或组有权以独占方式访问的对象。|  
|**adRightExecute**|536870912 (&AMP; H20000000)|用户或组有权执行对象。|  
|**adRightFull**|268435456 (&AMP; H10000000)|用户或组对象上具有所有权限。|  
|**adRightInsert**|32768 (&AMP; H8000)|用户或组有权插入该对象。 如对象**表**，用户有权将数据插入表。|  
|**adRightMaximumAllowed**|33554432 (&AMP; H 2000000)|用户或组有权限提供程序允许的最大的数目。 不依赖于提供程序的特定的权限。|  
|**adRightNone**|0|用户或组不具有权限的对象。|  
|**adRightRead**|-2147483648 (&H80000000)|用户或组有权读取对象。 如对象[表](../../../ado/reference/adox-api/table-object-adox.md)，用户有权读取表中的数据。|  
|**adRightReadDesign**|1024 (&AMP; H400)|用户或组有权读取对象的设计的。|  
|**adRightReadPermissions**|131072 (&AMP; H20000)|用户或组可以查看，但不是能更改在目录中的对象的特定权限。|  
|**adRightReference**|8192 (&AMP; H2000)|用户或组有权引用该对象。|  
|**adRightUpdate**|1073741824 (&AMP; H40000000)|用户或组有权更新的对象。 如对象**表**，用户有权更新表中的数据。|  
|**adRightWithGrant**|4096 (&AMP; H1000)|用户或组有权授予对象权限。|  
|**adRightWriteDesign**|2048 (&AMP; H800)|用户或组有权修改对象的设计的。|  
|**adRightWriteOwner**|524288 (&AMP; H80000)|用户或组有权修改对象的所有者。|  
|**adRightWritePermissions**|262144 (&AMP; H40000)|用户或组可以修改在目录中的对象的特定权限。|  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[GetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)|[SetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)|
