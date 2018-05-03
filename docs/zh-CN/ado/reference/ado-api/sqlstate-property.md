---
title: SQLState 属性 |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::GetSQLState
- Error::SQLState
- Error::get_SQLState
helpviewer_keywords:
- SQLState property
ms.assetid: f9e25967-54b0-444d-af2a-0d2c75365d3e
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ef960c158bb362798162a5d8e6a7e91f81961fa0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlstate-property"></a>SQLState 属性
指示 SQL 状态给定[错误](../../../ado/reference/ado-api/error-object.md)对象。  
  
## <a name="return-value"></a>返回值  
 返回五个字符**字符串**遵循 ANSI SQL 标准，表示的错误代码的值。  
  
## <a name="remarks"></a>注释  
 使用**SQLState**属性来读取该提供程序返回的 SQL 语句在处理过程中发生错误时的五个字符的错误代码。 例如，对于 ODBC 使用 Microsoft SQL Server 数据库的 Microsoft OLE DB 提供程序，当 SQL 状态错误代码来源于 ODBC，根据特定于 ODBC 的错误或错误来源于 Microsoft SQL Server，并为随后映射到 ODBC错误。 这些错误代码记录在 ANSI SQL 标准，但可能由不同的数据源以不同方式实现。  
  
## <a name="applies-to"></a>适用范围  
 [错误对象](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>另请参阅  
 [描述、 HelpContext、 HelpFile、 NativeError、 数量、 源和 SQLState 属性示例 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [描述、 HelpContext、 HelpFile、 NativeError、 数量、 源和 SQLState 属性示例 （VC + +）](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
