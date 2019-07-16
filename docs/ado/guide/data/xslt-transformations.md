---
title: XSLT 转换 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- XSLT transformations in ADO
ms.assetid: 1a46196e-839f-4734-a59e-2c64609ffb9e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2606733b3efc5a9641f8de0f544b3cff7c7e9a31
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923344"
---
# <a name="xslt-transformations"></a>XSLT 转换
XSLT 可以应用于生成的 XML，以将其转换为另一种格式。 了解在 ADO 中的 XML 格式时，可帮助开发 XSLT 模板，可以将它转换为更加用户友好格式。  
  
 例如，您知道，记录集的每一行另存为 rs： 数据元素内的 z： 行元素。 同样，每个字段的记录集另存为此元素的属性-值对。  
  
## <a name="remarks"></a>备注  
 以下 XSLT 脚本可以应用于要在浏览器中显示的 XML 显示上一节中将其转换为 HTML 表：  
  
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
  
 XSLT 转换为 HTML 表，其中显示了每个字段以及表标题记录集的 ADO Save 方法生成的 XML 流。 表标题和行也都指定不同的字体和颜色。  
  
## <a name="see-also"></a>请参阅  
 [以 XML 格式保留记录](../../../ado/guide/data/persisting-records-in-xml-format.md)
