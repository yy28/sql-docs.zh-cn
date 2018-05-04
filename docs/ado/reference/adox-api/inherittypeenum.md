---
title: InheritTypeEnum |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
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
ms.openlocfilehash: d4d822bd48d399b767c6676e014abe3d733aa5bc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
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
