---
title: ADO Java 类包装 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- class wrappers [ADO]
ms.assetid: 1fc09dc1-9e32-412e-9f43-b8eb8bb483ca
author: rothja
ms.author: jroth
ms.openlocfilehash: 485c53645387e5dafbe562442ec12503df0a6737
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760553"
---
# <a name="ado-java-class-wrappers"></a>ADO Java 类包装器
此代码声明了 ADO[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)类包装的实例，并将其初始化，所有代码都在相同的代码行中。 此外，它还声明[Open](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法中每个参数的变量，尤其是对于[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)和[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) （因为 Java 不支持枚举类型）。 它将打开并关闭**Recordset**对象。 将 Rs1 设置为 NULL 仅计划在 Java 对未使用的对象执行其系统化和间歇性释放时要释放的变量。  
  
```java
public static void main( String args[])  
{  
   msado15._Recordset   Rs1 = new msado15.Recordset();  
   Variant Source     = new Variant( "SELECT * FROM Authors" );  
   Variant Connect    = new Variant( "DSN=AdoDemo;UID=admin;PWD=;" );  
   int     LockType   = msado15.CursorTypeEnum.adOpenForwardOnly;  
   int     CursorType = msado15.LockTypeEnum.adLockReadOnly;  
   int     Options    = -1;  
  
   Rs1.Open( Source, Connect, LockType,  CursorType, Options );  
   Rs1.Close();  
   Rs1 = null;  
  
   System.out.println( "Success!\n" );  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [使用 Java 适用的 Microsoft SDK](../../../ado/guide/appendixes/using-the-microsoft-sdk-for-java.md)
