---
title: InheritTypeEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- InheritTypeEnum
helpviewer_keywords:
- InheritTypeEnum enumeration [ADOX]
ms.assetid: c2f6ce79-c4b3-4d40-ac95-21025208f991
author: MightyPen
ms.author: genemi
ms.openlocfilehash: aef8f768dd991e4e6ed740cc56600a6f1a8020e0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67965959"
---
# <a name="inherittypeenum"></a>InheritTypeEnum
指定对象如何继承权限集与[SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md)。  
  
|常量|ReplTest1|描述|  
|--------------|-----------|-----------------|  
|**adInheritBoth**|3|对象和其他容器所包含的主要对象将继承该条目。|  
|**adInheritContainers**|2|主要对象所包含的其他容器继承该条目。|  
|**adInheritNone**|0|默认值。 不发生继承。|  
|**adInheritNoPropagate**|4|**AdInheritObjects**并**adInheritContainers**标志不会传播到继承的条目。|  
|**adInheritObjects**|1|在容器中的非容器对象继承的权限。|  
  
## <a name="applies-to"></a>适用范围  
 [SetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)
