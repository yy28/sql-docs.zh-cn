---
description: InheritTypeEnum
title: InheritTypeEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 37c6eba57eb7efb05d2b718e294e33b9616cac77
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88984098"
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