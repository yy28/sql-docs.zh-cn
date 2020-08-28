---
description: ChangePassword 方法 (ADOX)
title: ChangePassword)  (ADOX 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _User25::raw_ChangePassword
- _User25::ChangePassword
helpviewer_keywords:
- ChangePassword method [ADOX]
ms.assetid: d187fbc6-5fac-4abb-803d-bf344dcf0302
author: rothja
ms.author: jroth
ms.openlocfilehash: e51037f9838e9aef279351c822e6c35ffb25f0fb
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985198"
---
# <a name="changepassword-method-adox"></a>ChangePassword 方法 (ADOX)
更改 [用户](./user-object-adox.md) 帐户的密码。  
  
## <a name="syntax"></a>语法  
  
```  
  
User.ChangePassword OldPassword, NewPassword  
```  
  
#### <a name="parameters"></a>参数  
 *OldPassword*  
 一个指定用户的现有密码的 **字符串** 值。 如果用户当前没有密码，请为 *OldPassword*使用空字符串 ( "" ) 。  
  
 *NewPassword*  
 一个指定新密码的 **字符串** 值。  
  
## <a name="remarks"></a>注解  
 出于安全原因，除了新密码之外，还必须指定旧密码。  
  
 如果提供程序不支持管理受信者属性，则会发生错误。  
  
## <a name="applies-to"></a>适用于  
 [用户对象 (ADOX)](./user-object-adox.md)  
  
## <a name="see-also"></a>另请参阅  
 [组和用户 Append、ChangePassword 方法示例 (VB)](./groups-and-users-append-changepassword-methods-example-vb.md)