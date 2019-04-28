---
title: ADO Java 类包装器 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ddcbba246f0bdcfb5c3a22766f5d335a2bd5893e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62719972"
---
# <a name="ado-java-class-wrappers"></a>ADO Java 类包装器
此代码声明了 ADO 的实例[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)类包装器，并初始化它，所有内容位于相同的代码行。 此外，为每个中的参数声明的变量[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法，尤其是对于[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)并[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) （由于 Java 不支持枚举类型）。 它打开和关闭**记录集**对象。 只设置为 NULL 的 Rs1 计划 Java 执行系统和间歇性发布的未使用的对象时释放该变量。  
  
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
  
## <a name="see-also"></a>请参阅  
 [使用 Java 适用的 Microsoft SDK](../../../ado/guide/appendixes/using-the-microsoft-sdk-for-java.md)
