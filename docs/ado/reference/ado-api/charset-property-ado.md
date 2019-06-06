---
title: Charset 属性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Charset
helpviewer_keywords:
- Charset property [ADO]
ms.assetid: e42507cb-9b46-4ce4-8191-2948eaf14ca2
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: da9e41d594890b399be975a9f1465a6bff50010a
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66698802"
---
# <a name="charset-property-ado"></a>Charset 属性 (ADO)
指示设置到其中的字符的文本内容[Stream](../../../ado/reference/ado-api/stream-object-ado.md)应为存储中的内部缓冲区的翻译**Stream**对象。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**字符串**指定的字符的值设置到其中的内容**Stream**将被转换。 默认值是**Unicode**。 允许的值是通过该接口作为 Internet 字符集名称 （例如，"iso-8859-1"、"Windows-1252"等） 传递的典型字符串。 由系统已知的字符组名称的列表，请参阅 HKEY_CLASSES_ROOT\MIME\Database\Charset Windows 注册表中的子项。  
  
## <a name="remarks"></a>备注  
 在文本中**Stream**对象，文本数据存储在由指定的字符集**字符集**属性。 默认值为 Unicode。 **Charset**属性用于转换数据传入**Stream**或带即将推出**Stream**。 例如，如果**Stream**包含 ISO-8859-1 数据和数据复制到一个 BSTR **Stream**对象会将数据转换为 Unicode。 反之亦然。  
  
 打开**Stream**，当前[位置](../../../ado/reference/ado-api/position-property-ado.md)必须是开头**Stream** (0)，以便能够设置**字符集**。  
  
 **Charset**仅用于文本**Stream**对象 ([类型](../../../ado/reference/ado-api/type-property-ado-stream.md)是**adTypeText**)。 如果忽略此属性**类型**是**adTypeBinary**。  
  
 代码示例，请参阅[步骤 4:详细信息文本框中填充](../../../ado/guide/data/step-4-populate-the-details-text-box.md)。  
  
## <a name="applies-to"></a>适用范围  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
