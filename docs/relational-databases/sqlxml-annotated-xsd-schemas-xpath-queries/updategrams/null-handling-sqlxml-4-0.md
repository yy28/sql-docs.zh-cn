---
title: NULL 处理 (SQLXML 4.0) |Microsoft 文档
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- updg:nullvalue attribute
- updategrams [SQLXML], null values
- nullvalue attribute
- null values [SQLXML]
ms.assetid: 5e11eebb-d94e-4ce6-a6d0-870225706bc1
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b53c3516dbe0ee87e23e9cb13ec441ef82a499c8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32968892"
---
# <a name="null-handling-sqlxml-40"></a>NULL 处理 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XML 语法将 NULL 视为不存在。 （例如，如果属性或元素值是 NULL，则该属性或元素不出现在 XML 文档中。）在[!INCLUDE[msCoName](../../../includes/msconame-md.md)]SQLXML， **updg:nullvalue**特性允许元素或属性的值指定 NULL。  
  
 例如，以下属的 updategram 确保**标题**值与联系人**ContactID** 64 个为 NULL，，然后更新**标题**"Mr."的值 为此联系人。  
  
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
  
 参数传递到 Updategram 时，NULL 可以作为参数值进行传递。 这可通过指定**nullvalue**属性中 **\<updg:header >** 块。 有关示例，请参阅[Passing Parameters to Updategram &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/passing-parameters-to-updategrams-sqlxml-4-0.md)。  
  
## <a name="see-also"></a>另请参阅  
 [属的 Updategram 安全注意事项&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
