---
description: ChangePassword 方法 (ADOX)
title: ChangePassword)  (ADOX 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
ms.openlocfilehash: 94ddd75bddf8845012fe0845826eea264718cc91
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2020
ms.locfileid: "88771166"
---
# <a name="changepassword-method-adox"></a>ChangePassword 方法 (ADOX)
更改 [用户](./user-object-adox.md) 帐户的密码。  
  
## <a name="syntax"></a>语法  
  
```  
  
User.ChangePassword OldPassword, NewPassword  
```  
  
#### <a name="parameters"></a>parameters  
 *OldPassword*  
 一个指定用户的现有密码的 **字符串** 值。 如果用户当前没有密码，请为 *OldPassword*使用空字符串 ( "" ) 。  
  
 *NewPassword*  
 一个指定新密码的 **字符串** 值。  
  
## <a name="remarks"></a>备注  
 出于安全原因，除了新密码之外，还必须指定旧密码。  
  
 如果提供程序不支持管理受信者属性，则会发生错误。  
  
## <a name="applies-to"></a>适用于  
 [用户对象 (ADOX)](./user-object-adox.md)  
  
## <a name="see-also"></a>另请参阅  
 [组和用户 Append、ChangePassword 方法示例 (VB)](./groups-and-users-append-changepassword-methods-example-vb.md)