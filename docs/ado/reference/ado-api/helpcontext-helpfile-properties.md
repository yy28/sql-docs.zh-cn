---
title: HelpContext、 HelpFile 属性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::GetHelpContext
- Error::GetHelpFile
- Error::get_HelpFile
- Error::get_HelpContext
- Error::HelpContext
- Error::HelpFile
helpviewer_keywords:
- HelpContext property [ADO]
- HelpFile property [ADO]
ms.assetid: 2b9ef441-993c-44d4-8f87-fac0979dac1d
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c9c980e293b06e7fa9642ace7d425b7ffd3c0197
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66694803"
---
# <a name="helpcontext-helpfile-properties"></a>HelpContext、HelpFile 属性
指示的帮助文件和主题与相关联[错误](../../../ado/reference/ado-api/error-object.md)对象。  
  
## <a name="return-values"></a>返回值  
  
-   **帮助上下文 Id**返回的上下文 ID，作为**长**值，用于帮助文件中的主题。  
  
-   **HelpFile**返回**字符串**的计算结果为指向帮助文件的完全解析路径的值。  
  
## <a name="remarks"></a>备注  
 如果帮助文件中指定**HelpFile**属性， **HelpContext**属性用于自动显示其标识的帮助主题。 如果没有任何相关的帮助主题可用，则**HelpContext**属性将返回零并且**HelpFile**属性返回一个零长度字符串 ("")。  
  
## <a name="applies-to"></a>适用范围  
 [错误对象](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>请参阅  
 [Description、 HelpContext、 HelpFile、 NativeError、 数、 源和 SQLState 属性示例 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Description、 HelpContext、 HelpFile、 NativeError、 数、 源和 SQLState 属性示例 （VC + +）](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Description 属性](../../../ado/reference/ado-api/description-property.md)   
 [Number 属性 (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [Source 属性（ADO 错误）](../../../ado/reference/ado-api/source-property-ado-error.md)
