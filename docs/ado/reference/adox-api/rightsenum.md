---
title: RightsEnum |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: b49fbddab49266ee5a5d530867c281e72878b6d7
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/22/2020
ms.locfileid: "86943019"
---
# <a name="rightsenum"></a>RightsEnum
指定组或用户对对象的权限。  
  
|返回的常量|值|说明|  
|--------------|-----------|-----------------|  
|**adRightCreate**|16384（&H4000）|用户或组具有创建此类型的新对象的权限。|  
|**adRightDelete**|65536（&H10000）|用户或组有权删除对象中的数据。 对于**表**等对象，用户有权从记录中删除数据值。|  
|**adRightDrop**|256（&H100）|用户或组有权从目录中删除对象。 例如，DROP TABLE SQL 命令可以删除**表**。|  
|**adRightExclusive**|512（&H200）|用户或组有权仅访问该对象。|  
|**adRightExecute**|536870912（&H20000000）|用户或组具有执行对象的权限。|  
|**adRightFull**|268435456（&H10000000）|用户或组具有对对象的所有权限。|  
|**adRightInsert**|32768（&H8000）|用户或组有权插入对象。 对于**表**等对象，用户有权将数据插入表中。|  
|**adRightMaximumAllowed**|33554432（&H2000000）|用户或组具有提供程序允许的最大权限数。 特定权限与提供程序相关。|  
|**adRightNone**|0|用户或组对该对象没有任何权限。|  
|**adRightRead**|-2147483648 （&H80000000）|用户或组有权读取对象。 对于[表](../../../ado/reference/adox-api/table-object-adox.md)等对象，用户有权读取表中的数据。|  
|**adRightReadDesign**|1024（&H400）|用户或组有权读取对象的设计。|  
|**adRightReadPermissions**|131072（&H20000）|用户或组可以查看但不能更改目录中对象的特定权限。|  
|**adRightReference**|8192（&H2000）|用户或组有权引用该对象。|  
|**adRightUpdate**|1073741824（&H40000000）|用户或组具有更新该对象的权限。 对于**表**等对象，用户有权更新表中的数据。|  
|**adRightWithGrant**|4096（&H1000）|用户或组有权授予对对象的权限。|  
|**adRightWriteDesign**|2048（&H800）|用户或组有权修改对象的设计。|  
|**adRightWriteOwner**|524288（&H80000）|用户或组有权修改对象的所有者。|  
|**adRightWritePermissions**|262144（&H40000）|用户或组可以修改目录中对象的特定权限。|  
  
## <a name="applies-to"></a>应用到  

:::row:::
    :::column:::
        [GetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)  
    :::column-end:::
    :::column:::
        [SetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)  
    :::column-end:::
:::row-end:::
