---
title: "XSLT 转换 |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XSLT transformations in ADO
ms.assetid: 1a46196e-839f-4734-a59e-2c64609ffb9e
caps.latest.revision: 3
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 36b39d14a4856d882add1e9bafdc9457fa3b8bc1
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="xslt-transformations"></a>XSLT 转换
可将 XSLT 应用到生成的 XML 将其转换为另一种格式。 了解在 ADO 中的 XML 格式可帮助在开发可以将它转换为更加友好的用户的窗体的 XSLT 模板。  
  
 例如，你知道记录集的每个行被另存为 rs： 数据元素内的 z： 行元素。 同样，每个字段的记录集保存为此元素的属性值对。  
  
## <a name="remarks"></a>注释  
 以下的 XSLT 脚本可以应用到显示上一节中将其转换成 HTML 表的 XML，在浏览器中显示：  
  
```  
<?xml version="1.0" encoding="ISO-8859-1"?>  
<html xmlns:xsl="http://www.w3.org/TR/WD-xsl">  
<body STYLE="font-family:Arial, helvetica, sans-serif; font-size:12pt; background-color:white">  
<table border="1" style="table-layout:fixed" width="600">  
  <col width="200"></col>  
  <tr bgcolor="teal">  
    <th><font color="white">CustomerId</font></th>  
    <th><font color="white">CompanyName</font></th>  
    <th><font color="white">ContactName</font></th>  
  </tr>  
<xsl:for-each select="xml/rs:data/z:row">  
  <tr bgcolor="navy">  
    <td><font color="white"><xsl:value-of select="@CustomerID"/></font></td>  
    <td><font color="white"><xsl:value-of select="@CompanyName"/></font></td>  
    <td><font color="white"><xsl:value-of select="@ContactName"/></font></td>   
  </tr>  
</xsl:for-each>  
</table>  
</body>  
</html>  
```  
  
 XSLT 将转换到一个 HTML 表，它显示每个字段的记录集以及表标题 ADO 保存方法生成的 XML 流。 表标题和行也被分配不同的字体和颜色。  
  
## <a name="see-also"></a>另请参阅  
 [保留记录采用 XML 格式](../../../ado/guide/data/persisting-records-in-xml-format.md)
