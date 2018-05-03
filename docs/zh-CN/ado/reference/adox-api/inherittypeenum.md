---
title: InheritTypeEnum |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- InheritTypeEnum
helpviewer_keywords:
- InheritTypeEnum enumeration [ADOX]
ms.assetid: c2f6ce79-c4b3-4d40-ac95-21025208f991
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 443a57c6e1197aa36348e89e6cec1d9a3989b24c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="inherittypeenum"></a>InheritTypeEnum
指定对象如何继承权限集与[SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md)。  
  
|常量|“值”|Description|  
|--------------|-----------|-----------------|  
|**adInheritBoth**|3|对象和主对象中包含的其他容器将继承该条目。|  
|**adInheritContainers**|2|主要对象中包含其他容器继承该项。|  
|**adInheritNone**|0|默认值。 不发生继承。|  
|**adInheritNoPropagate**|4|**AdInheritObjects**和**adInheritContainers**标志不会传播到继承的条目。|  
|**adInheritObjects**|1|容器中的非容器对象继承的权限。|  
  
## <a name="applies-to"></a>适用范围  
 [SetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)
