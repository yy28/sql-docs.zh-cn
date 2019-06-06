---
title: ChangePassword 方法 (ADOX) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 981f2e5b801cd35b0aedb04e5f1aa11b741e4535
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66708002"
---
# <a name="changepassword-method-adox"></a>ChangePassword 方法 (ADOX)
更改的密码[用户](../../../ado/reference/adox-api/user-object-adox.md)帐户。  
  
## <a name="syntax"></a>语法  
  
```  
  
User.ChangePassword OldPassword, NewPassword  
```  
  
#### <a name="parameters"></a>Parameters  
 *OldPassword*  
 一个**字符串**值，该值指定用户的现有密码。 如果用户当前没有密码，则使用空字符串 ("") 的*OldPassword*。  
  
 *NewPassword*  
 一个**字符串**值，该值指定新密码。  
  
## <a name="remarks"></a>备注  
 出于安全原因，除了新密码必须指定旧密码。  
  
 如果提供程序不支持的受信者属性的管理，将会出错。  
  
## <a name="applies-to"></a>适用范围  
 [用户对象 (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)  
  
## <a name="see-also"></a>请参阅  
 [组和用户 Append、ChangePassword 方法示例 (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)
