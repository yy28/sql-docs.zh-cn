---
description: InheritTypeEnum
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
author: rothja
ms.author: jroth
ms.openlocfilehash: dfa4d6c15cc7d26dbfe964947bd09a04e2f75128
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88439849"
---
# <a name="inherittypeenum"></a>InheritTypeEnum
指定对象如何继承具有 [SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md)的权限集。  
  
|返回的常量|值|描述|  
|--------------|-----------|-----------------|  
|**adInheritBoth**|3|对象和主对象所包含的其他容器都继承该条目。|  
|**adInheritContainers**|2|主对象包含的其他容器继承该条目。|  
|**adInheritNone**|0|默认。 不发生继承。|  
|**adInheritNoPropagate**|4|**AdInheritObjects**和**adInheritContainers**标志不会传播到继承的项。|  
|**adInheritObjects**|1|容器中的非容器对象将继承权限。|  
  
## <a name="applies-to"></a>适用于  
 [SetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)
