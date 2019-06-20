---
title: NULL 处理 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- updg:nullvalue attribute
- updategrams [SQLXML], null values
- nullvalue attribute
- null values [SQLXML]
ms.assetid: 5e11eebb-d94e-4ce6-a6d0-870225706bc1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 11f7ca96ca65ae23202b84030140e0eaef945de2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66014689"
---
# <a name="null-handling-sqlxml-40"></a>NULL 处理 (SQLXML 4.0)
  XML 语法将 NULL 视为不存在。 (例如，如果属性或元素值为 NULL，该属性或元素不存在从 XML 文档。)在中[!INCLUDE[msCoName](../../../includes/msconame-md.md)]SQLXML，`updg:nullvalue`特性使元素或属性值指定为 NULL。  
  
 例如，以下 updategram 确保**标题**值与联系人**ContactID** 64 的为 NULL，并更新**标题**值为"Mr." 该联系人。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync updg:nullvalue="IsNULL"  >  
    <updg:before>  
       <Person.Contact ContactID="64" Title="IsNULL" />  
    </updg:before>  
    <updg:after>  
       <Person.Contact ContactID="64" Title="Mr." />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 参数传递到 Updategram 时，NULL 可以作为参数值进行传递。 通过在 `nullvalue` 块中指定 `<updg:header>` 属性，可以完成该操作。 有关示例，请参阅[将参数传递给 Updategram &#40;SQLXML 4.0&#41;](passing-parameters-to-updategrams-sqlxml-4-0.md)。  
  
## <a name="see-also"></a>请参阅  
 [Updategram 安全注意事项&#40;SQLXML 4.0&#41;](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
