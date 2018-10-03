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
manager: craigg
ms.openlocfilehash: 96268fac4b81230fcb63db6b48ef4ef794abb9c7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47788705"
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
