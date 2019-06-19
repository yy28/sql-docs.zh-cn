---
title: RightsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RightsEnum
helpviewer_keywords:
- RightsEnum enumeration [ADOX]
ms.assetid: 55ee67c7-a583-42aa-849a-78264b4cb614
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a34cbd8ee3d274d3b3d45049611ca9cc99fa7758
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66718835"
---
# <a name="rightsenum"></a>RightsEnum
指定对某个对象的权限或组或用户权限。  
  
|常量|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**adRightCreate**|16384 (&H4000)|用户或组有权创建此类型的新对象。|  
|**adRightDelete**|65536 (&H10000)|用户或组有权从对象中删除数据。 如对象**表**，用户有权从记录中删除数据值。|  
|**adRightDrop**|256 (&H100)|用户或组有权从目录删除对象。 例如，**表**可以通过删除表 SQL 命令来删除。|  
|**adRightExclusive**|512 (H200）|用户或组有权以独占方式访问的对象。|  
|**adRightExecute**|536870912 (&H20000000)|用户或组有权执行对象。|  
|**adRightFull**|268435456 (&H10000000)|用户或组对对象具有所有权限。|  
|**adRightInsert**|32768 (&H8000)|用户或组已插入该对象的权限。 如对象**表**，用户有权将数据插入到表。|  
|**adRightMaximumAllowed**|33554432 (&AMP; H 2000000)|用户或组具有允许提供程序的权限的最大数目。 提供程序依赖于特定的权限。|  
|**adRightNone**|0|用户或组具有对该对象没有任何权限。|  
|**adRightRead**|-2147483648 (&H80000000)|用户或组有权读取的对象。 如对象[表](../../../ado/reference/adox-api/table-object-adox.md)，用户有权读取表中的数据。|  
|**adRightReadDesign**|1024 (&AMP; H400)|用户或组有权读取对象的设计的。|  
|**adRightReadPermissions**|131072 (H20000）|用户或组可以查看，但不是更改，请在目录中的对象的特定权限。|  
|**adRightReference**|8192 (&AMP; H2000)|用户或组具有引用该对象的权限。|  
|**adRightUpdate**|1073741824 (&H40000000)|用户或组有权更新的对象。 如对象**表**，用户有权更新表中的数据。|  
|**adRightWithGrant**|4096 (&H1000)|用户或组有权授予对对象的权限。|  
|**adRightWriteDesign**|2048 (&AMP; H800)|用户或组有权修改对象的设计的。|  
|**adRightWriteOwner**|524288 (&H80000)|用户或组有权修改的对象的所有者。|  
|**adRightWritePermissions**|262144 (&H40000)|用户或组可以修改在目录中的对象的特定权限。|  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[GetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)|[SetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)|
