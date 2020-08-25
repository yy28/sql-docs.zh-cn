---
description: ActionEnum
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 2c9032dfdb3394e582541f60afce7b930751a5c0
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777776"
---
# <a name="actionenum"></a>ActionEnum
指定在调用 [SetPermissions](./setpermissions-method-adox.md) 时要执行的操作的类型。  
  
|返回的常量|Value|说明|  
|--------------|-----------|-----------------|  
|**adAccessDeny**|3|该组或用户将被拒绝指定的权限。|  
|**adAccessGrant**|1|该组或用户将至少具有所需的权限。|  
|**adAccessRevoke**|4|组或用户的所有显式访问权限将被吊销。|  
|**adAccessSet**|2|该组或用户将拥有完全请求的权限。|