---
title: NativeError 属性 (ADO) |Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 17f279af526a9e1f5b2c8deff4b4092e7949c5ea
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66707262"
---
# <a name="nativeerror-property-ado"></a>NativeError 属性 (ADO)
指示提供程序特定错误代码为给定[错误](../../../ado/reference/ado-api/error-object.md)对象。  
  
## <a name="return-value"></a>返回值  
 返回**长**值，该值指示错误代码。  
  
## <a name="remarks"></a>备注  
 使用**NativeError**属性来检索特定的数据库特定错误信息**错误**对象。 例如，当使用 Microsoft ODBC 访问接口用于 OLE DB 和 Microsoft SQL Server 数据库，来源于 SQL Server 的本机错误代码通过 ODBC 和 ODBC 访问接口进入 ADO **NativeError**属性。  
  
## <a name="applies-to"></a>适用范围  
 [错误对象](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>请参阅  
 [Description、 HelpContext、 HelpFile、 NativeError、 数、 源和 SQLState 属性示例 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Description、 HelpContext、 HelpFile、 NativeError、 数、 源和 SQLState 属性示例 （VC + +）](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
