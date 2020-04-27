---
title: NativeError 属性（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::GetNativeError
- Error::get_NativeError
- Error::NativeError
helpviewer_keywords:
- NativeError property [ADO]
ms.assetid: b9b47e57-18a4-4186-aef5-5bd18d7b1d74
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 42888190dcd7b5e41987e6e8ec7194242549aa9c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "67918019"
---
# <a name="nativeerror-property-ado"></a>NativeError 属性 (ADO)
指示给定[错误](../../../ado/reference/ado-api/error-object.md)对象的特定于提供程序的错误代码。  
  
## <a name="return-value"></a>返回值  
 返回指示错误代码的**Long**值。  
  
## <a name="remarks"></a>备注  
 使用**NativeError**属性检索特定**错误**对象的数据库特定的错误信息。 例如，将 Microsoft ODBC 提供程序用于 OLE DB 与 Microsoft SQL Server 数据库一起使用时，源自 SQL Server 将 ODBC 和 ODBC 提供程序传递到 ADO **NativeError**属性的本机错误代码。  
  
## <a name="applies-to"></a>应用于  
 [Error 对象](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>另请参阅  
 [Description、HelpContext、帮助，NativeError、Number、Source 和 SQLState 属性示例（VB）](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Description、HelpContext、帮助，NativeError、Number、Source 和 SQLState 属性示例（VC + +）](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
