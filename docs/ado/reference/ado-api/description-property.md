---
title: Description 属性 |Microsoft Docs
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
ms.openlocfilehash: 48b3a6987e6c7b6c3754f5041d90d248520345ab
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67933080"
---
# <a name="description-property"></a>Description 属性
描述[错误](../../../ado/reference/ado-api/error-object.md)对象。  
  
## <a name="return-value"></a>返回值  
 返回一个**字符串**值，该值包含对错误的说明。  
  
## <a name="remarks"></a>备注  
 使用**Description**属性可获取错误的简短说明。 显示此属性以提醒用户无法或不想处理的错误。 该字符串来自 ADO 或提供程序。  
  
 提供程序负责向 ADO 传递特定的错误文本。 ADO 将[错误](../../../ado/reference/ado-api/error-object.md)对象添加到每个提供程序错误或它收到的警告的**错误**集合中。 枚举**errors**集合以跟踪提供程序传递的错误。  
  
## <a name="applies-to"></a>应用于  
 [错误对象](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>另请参阅  
 [Description、HelpContext、帮助，NativeError、Number、Source 和 SQLState 属性示例（VB）](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Description、HelpContext、帮助，NativeError、Number、Source 和 SQLState 属性示例（VC + +）](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [HelpContext，帮助的属性](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Number 属性（ADO）](../../../ado/reference/ado-api/number-property-ado.md)   
 [Source 属性（ADO 错误）](../../../ado/reference/ado-api/source-property-ado-error.md)
