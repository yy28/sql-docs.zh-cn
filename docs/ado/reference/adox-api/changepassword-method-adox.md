---
title: "ChangePassword 方法 (ADOX) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _User25::raw_ChangePassword
- _User25::ChangePassword
helpviewer_keywords: ChangePassword method [ADOX]
ms.assetid: d187fbc6-5fac-4abb-803d-bf344dcf0302
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4df8c533048ae51662369b66361fb6b642c97f03
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="changepassword-method-adox"></a>ChangePassword 方法 (ADOX)
更改密码[用户](../../../ado/reference/adox-api/user-object-adox.md)帐户。  
  
## <a name="syntax"></a>语法  
  
```  
  
User.ChangePassword OldPassword, NewPassword  
```  
  
#### <a name="parameters"></a>Parameters  
 *旧密码*  
 A**字符串**值，该值指定用户的现有密码。 如果用户当前没有密码，使用空字符串 ("") 为*OldPassword*。  
  
 *新密码*  
 A**字符串**值，该值指定新密码。  
  
## <a name="remarks"></a>Remarks  
 出于安全原因，除了新密码必须指定旧密码。  
  
 如果提供程序不支持的受信者属性的管理，将会出错。  
  
## <a name="applies-to"></a>适用范围  
 [用户对象 (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)  
  
## <a name="see-also"></a>另请参阅  
 [组和用户 Append、ChangePassword 方法示例 (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)
