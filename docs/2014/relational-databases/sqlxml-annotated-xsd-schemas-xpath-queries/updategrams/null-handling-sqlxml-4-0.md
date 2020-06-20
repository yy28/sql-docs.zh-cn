---
title: NULL 处理（SQLXML 4.0） |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 430643e8a6c9bd3dd00b2763990645c6a162ee40
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85047493"
---
# <a name="null-handling-sqlxml-40"></a>NULL 处理 (SQLXML 4.0)
  XML 语法将 NULL 视为不存在。 （例如，如果属性或元素值为 NULL，则 XML 文档中不存在该属性或元素。）在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 中， `updg:nullvalue` 特性允许为元素或属性值指定 NULL。  
  
 例如，以下 updategram 确保**ContactID**为64的联系人的**标题**值为 NULL，然后将**Title**值更新为 "Mr"。 此联系人。  
  
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
  
 参数传递到 Updategram 时，NULL 可以作为参数值进行传递。 通过在 `nullvalue` 块中指定 `<updg:header>` 属性，可以完成该操作。 有关示例，请参阅[将参数传递到 updategram &#40;SQLXML 4.0&#41;](passing-parameters-to-updategrams-sqlxml-4-0.md)。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;SQLXML 4.0&#41;的 Updategram 安全注意事项](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
