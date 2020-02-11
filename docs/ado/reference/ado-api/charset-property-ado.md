---
title: 字符集属性（ADO） |Microsoft Docs
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
ms.openlocfilehash: 69d65a5330ea83b955629cd9de9684ecc47906ec
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67920085"
---
# <a name="charset-property-ado"></a>Charset 属性 (ADO)
指示一个字符集，文本[流](../../../ado/reference/ado-api/stream-object-ado.md)的内容应在**流**对象的内部缓冲区中转换为存储。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回一个**字符串**值，该值指定将转换**流**内容的字符集。 默认值为**Unicode**。 允许的值是作为 Internet 字符集名称传递的典型字符串（例如，"iso-8859-1"、"Windows-1252" 等）。 有关系统已知的字符集名称列表，请参阅 Windows 注册表中 HKEY_CLASSES_ROOT \MIME\Database\Charset 的子项。  
  
## <a name="remarks"></a>备注  
 在文本**流**对象中，文本数据存储在**字符集属性指定的字符集**中。 默认值为 Unicode。 **字符集**属性用于将数据转换为**流**中或**流**出的数据。 例如，如果**流**包含 ISO-8859-1 数据，并且将数据复制到 BSTR，则**流**对象会将数据转换为 Unicode。 反之亦然。  
  
 对于打开的**流**，[当前位置必须位于](../../../ado/reference/ado-api/position-property-ado.md)**流**的开头（0），才能设置**字符集**。  
  
 **字符集**仅用于文本**流**对象（[类型](../../../ado/reference/ado-api/type-property-ado-stream.md)为**adTypeText**）。 如果**类型**是**adTypeBinary**，则忽略此属性。  
  
 有关代码示例，请参阅[步骤4：填充详细信息文本框](../../../ado/guide/data/step-4-populate-the-details-text-box.md)。  
  
## <a name="applies-to"></a>应用于  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
