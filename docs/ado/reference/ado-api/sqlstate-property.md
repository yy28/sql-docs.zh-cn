---
title: SQLState 属性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::GetSQLState
- Error::SQLState
- Error::get_SQLState
helpviewer_keywords:
- SQLState property
ms.assetid: f9e25967-54b0-444d-af2a-0d2c75365d3e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 00ab80a10b2c7c411cee0fb6061467d67cfbd4a2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62740357"
---
# <a name="sqlstate-property"></a>SQLState 属性
指示 SQL 状态的给定[错误](../../../ado/reference/ado-api/error-object.md)对象。  
  
## <a name="return-value"></a>返回值  
 返回 5 个字符**字符串**值，该值遵循 ANSI SQL 标准并指示错误代码。  
  
## <a name="remarks"></a>备注  
 使用**SQLState**要读取的提供程序返回的 SQL 语句处理期间发生错误时的五字符错误代码属性。 例如，使用 Microsoft OLE DB Provider for ODBC 与 Microsoft SQL Server 数据库时, 状态的 SQL 错误代码来源于 ODBC 中，基于特定于 ODBC 的错误或错误的来源于 Microsoft SQL Server，并已进行映射到 ODBC错误。 这些错误代码记录在 ANSI SQL 标准，但不同的数据源可能以不同方式实现。  
  
## <a name="applies-to"></a>适用范围  
 [错误对象](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>请参阅  
 [Description、 HelpContext、 HelpFile、 NativeError、 数、 源和 SQLState 属性示例 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Description、 HelpContext、 HelpFile、 NativeError、 数、 源和 SQLState 属性示例 （VC + +）](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
