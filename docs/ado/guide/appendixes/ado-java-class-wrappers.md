---
title: ADO Java 类包装器 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- class wrappers [ADO]
ms.assetid: 1fc09dc1-9e32-412e-9f43-b8eb8bb483ca
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 840d8a0e266a6f913a8a74ec1451bc6285fbb08b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47729215"
---
# <a name="ado-java-class-wrappers"></a>ADO Java 类包装器
此代码声明了 ADO 的实例[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)类包装器，并初始化它，所有内容位于相同的代码行。 此外，为每个中的参数声明的变量[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法，尤其是对于[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)并[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) （由于 Java 不支持枚举类型）。 它打开和关闭**记录集**对象。 只设置为 NULL 的 Rs1 计划 Java 执行系统和间歇性发布的未使用的对象时释放该变量。  
  
```  
public static void main( String args[])  
{  
   msado15._Recordset   Rs1 = new msado15.Recordset();  
   Variant Source     = new Variant( "SELECT * FROM Authors" );  
   Variant Connect    = new Variant( "DSN=AdoDemo;UID=admin;PWD=;" );  
   int     LockType   = msado15.CursorTypeEnum.adOpenForwardOnly;  
   int     CursorType = msado15.LockTypeEnum.adLockReadOnly;  
   int     Options    = -1;  
  
   Rs1.Open( Source, Connect, LockType,  CursorType, Options );  
   Rs1.Close();  
   Rs1 = null;  
  
   System.out.println( "Success!\n" );  
}  
```  
  
## <a name="see-also"></a>请参阅  
 [使用 Java 适用的 Microsoft SDK](../../../ado/guide/appendixes/using-the-microsoft-sdk-for-java.md)
