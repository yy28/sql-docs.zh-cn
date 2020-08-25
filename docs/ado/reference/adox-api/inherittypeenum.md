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
ms.openlocfilehash: d1fed614d90bbf53fdb2198e3ddd657a1e44acd1
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770116"
---
# <a name="inherittypeenum"></a>InheritTypeEnum
指定对象如何继承具有 [SetPermissions](./setpermissions-method-adox.md)的权限集。  
  
|返回的常量|Value|说明|  
|--------------|-----------|-----------------|  
|**adInheritBoth**|3|对象和主对象所包含的其他容器都继承该条目。|  
|**adInheritContainers**|2|主对象包含的其他容器继承该条目。|  
|**adInheritNone**|0|默认。 不发生继承。|  
|**adInheritNoPropagate**|4|**AdInheritObjects**和**adInheritContainers**标志不会传播到继承的项。|  
|**adInheritObjects**|1|容器中的非容器对象将继承权限。|  
  
## <a name="applies-to"></a>适用于  
 [SetPermissions 方法 (ADOX)](./setpermissions-method-adox.md)