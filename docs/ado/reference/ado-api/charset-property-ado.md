---
title: 字符集属性 (ADO) |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Charset
helpviewer_keywords:
- Charset property [ADO]
ms.assetid: e42507cb-9b46-4ce4-8191-2948eaf14ca2
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 972f090d648c94c3fab20f013eaa185fe3849f00
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="charset-property-ado"></a>字符集属性 (ADO)
指示设置到其中的字符文本的内容[流](../../../ado/reference/ado-api/stream-object-ado.md)的内部缓冲区中的存储转换应有**流**对象。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**字符串**指定的字符的值设置到其中的内容**流**将转换。 默认值是**Unicode**。 允许的值是该接口通过传递作为 Internet 字符集名称 （例如，"iso-8859-1"、"windows-1252"等） 的典型字符串。 由系统已知的字符组名称的列表，请参阅 HKEY_CLASSES_ROOT\MIME\Database\Charset Windows 注册表中的子项。  
  
## <a name="remarks"></a>注释  
 在文本中**流**对象，文本数据存储在由指定的字符集**Charset**属性。 默认值为 Unicode。 **Charset**属性用于将数据进入转换**流**或外接下来**流**。 例如，如果**流**包含 ISO 8859-1 数据和数据复制到 BSTR，**流**对象会将数据转换为 Unicode。 反之亦然。  
  
 已打开**流**，当前[位置](../../../ado/reference/ado-api/position-property-ado.md)必须是开头的**流**(0) 若要能够设置**Charset**。  
  
 **Charset**仅用于文本**流**对象 ([类型](../../../ado/reference/ado-api/type-property-ado-stream.md)是**adTypeText**)。 如果忽略此属性**类型**是**adTypeBinary**。  
  
 代码示例，请参阅[步骤 4： 详细信息的文本框中填充](../../../ado/guide/data/step-4-populate-the-details-text-box.md)。  
  
## <a name="applies-to"></a>适用范围  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
