---
title: 说明属性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::Description
- Error::GetDescription
- Error::get_Description
helpviewer_keywords:
- Description property
ms.assetid: 4b5d6790-6c29-42aa-bf78-d9cfb8ad7965
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7b743a5fb6673baf886c4b9327bd8ad93b00d3b1
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66698322"
---
# <a name="description-property"></a>Description 属性
介绍[错误](../../../ado/reference/ado-api/error-object.md)对象。  
  
## <a name="return-value"></a>返回值  
 返回**字符串**值，该值包含错误的说明。  
  
## <a name="remarks"></a>备注  
 使用**说明**属性来获取错误的简短说明。 显示此属性不能或不希望处理的错误向用户发出警报。 该字符串将来自 ADO 或提供程序。  
  
 提供商将负责将特定的错误文本传递给 ADO。 添加了 ADO[错误](../../../ado/reference/ado-api/error-object.md)对象传递给**错误**集合每个提供程序错误或警告它收到。 枚举**错误**集合，可以跟踪提供程序将传递的错误。  
  
## <a name="applies-to"></a>适用范围  
 [错误对象](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>请参阅  
 [Description、 HelpContext、 HelpFile、 NativeError、 数、 源和 SQLState 属性示例 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Description、 HelpContext、 HelpFile、 NativeError、 数、 源和 SQLState 属性示例 （VC + +）](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [HelpContext、 HelpFile 属性](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Number 属性 (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [Source 属性（ADO 错误）](../../../ado/reference/ado-api/source-property-ado-error.md)
