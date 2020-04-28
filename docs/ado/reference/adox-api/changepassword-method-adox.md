---
title: ChangePassword 方法（ADOX） |Microsoft Docs
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
ms.openlocfilehash: de8baf504a76407037322fd6b799f6d63584eae7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "67967034"
---
# <a name="changepassword-method-adox"></a>ChangePassword 方法 (ADOX)
更改[用户](../../../ado/reference/adox-api/user-object-adox.md)帐户的密码。  
  
## <a name="syntax"></a>语法  
  
```  
  
User.ChangePassword OldPassword, NewPassword  
```  
  
#### <a name="parameters"></a>参数  
 *OldPassword*  
 一个指定用户的现有密码的**字符串**值。 如果用户当前没有密码，请为*OldPassword*使用空字符串（""）。  
  
 *NewPassword*  
 一个指定新密码的**字符串**值。  
  
## <a name="remarks"></a>备注  
 出于安全原因，除了新密码之外，还必须指定旧密码。  
  
 如果提供程序不支持管理受信者属性，则会发生错误。  
  
## <a name="applies-to"></a>应用于  
 [用户对象 (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)  
  
## <a name="see-also"></a>另请参阅  
 [组和用户 Append、ChangePassword 方法示例 (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)
