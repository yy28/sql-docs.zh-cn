---
title: 命名空间 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- namespaces in ADO
ms.assetid: efff5569-db52-451d-a039-2e74870534da
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 0e04ffd13183462b0d2a5e68ebc177b8b342b570
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66701861"
---
# <a name="namespaces"></a>命名空间
XML 暂留格式在 ADO 中使用以下四个命名空间。  
  
## <a name="remarks"></a>备注  
 XML 暂留格式在 ADO 中使用以下四个命名空间。  
  
|Prefix|Description|  
|------------|-----------------|  
|s|引用包含的元素和属性定义当前记录集的架构的"XML 数据"命名空间。|  
|dt|引用的数据类型定义规范。|  
|rs|引用的命名空间包含元素和属性特定于 ADO 记录集属性和属性。|  
|z|引用的当前行集架构。|  
  
 客户端不应将其自身标记添加到这些命名空间，如规范所定义。 例如，客户端不应定义为一个命名空间"urn： 架构-microsoft-com:rowset"然后写出类似于"rs: MyOwnTag。" 若要了解有关命名空间的详细信息，请参阅[W3C XML 建议中的命名空间](http://www.w3.org/TR/REC-xml-names/)。  
  
> [!IMPORTANT]
>  架构标记的 ID 必须是"RowsetSchema，"并使用来指代当前行集的架构的命名空间必须指向"#RowsetSchema。"  
  
 请注意命名空间的冒号和等号之间的部分的前缀是任意的。  
  
```  
xmlns:rs="urn:schemas-microsoft-com:rowset"  
```  
  
 用户可以定义这是任何名称，只要整个 XML 文档一致地使用此名称。 ADO 始终写出"s、"rs、"dt，"并"z，"但这些前缀名称不是硬编码到加载组件。  
  
## <a name="see-also"></a>请参阅  
 [以 XML 格式保留记录](../../../ado/guide/data/persisting-records-in-xml-format.md)
