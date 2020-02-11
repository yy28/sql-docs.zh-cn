---
title: ActionEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ActionEnum
helpviewer_keywords:
- ActionEnum enumeration [ADOX]
ms.assetid: f948febd-c885-4621-823b-421e116fec4e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fad40c6daed6fd86f93da3f658af6a21c33ca762
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67928624"
---
# <a name="actionenum"></a>ActionEnum
指定在调用[SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md)时要执行的操作的类型。  
  
|一直|值|说明|  
|--------------|-----------|-----------------|  
|**adAccessDeny**|3|该组或用户将被拒绝指定的权限。|  
|**adAccessGrant**|1|该组或用户将至少具有所需的权限。|  
|**adAccessRevoke**|4|组或用户的所有显式访问权限将被吊销。|  
|**adAccessSet**|2|该组或用户将拥有完全请求的权限。|
