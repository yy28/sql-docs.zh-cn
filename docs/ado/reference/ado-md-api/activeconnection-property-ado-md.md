---
title: "ActiveConnection 属性 (ADO MD) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- ActiveConnection
- Cellset::ActiveConnection
- Catalog::ActiveConnection
helpviewer_keywords: ActiveConnection property [ADO MD]
ms.assetid: 2509b32c-a995-4364-9152-d8c83129bdd8
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2a3a25e63f4da0329e3b1f81ced1b2b4fbe4086c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="activeconnection-property-ado-md"></a>ActiveConnection 属性 (ADO MD)
指示哪些 ADO[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象的当前的单元集或当前所属的编录。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**Variant** ，其中包含定义连接字符串或**连接**对象。 默认值为空。  
  
## <a name="remarks"></a>注释  
 你可以将此属性设置为有效的 ADO**连接**对象或有效的连接字符串。 当此属性设置为连接字符串时，该提供程序创建一个新**连接**对象使用此定义，并打开该连接。  
  
 如果你使用*ActiveConnection*参数[打开](../../../ado/reference/ado-md-api/open-method-ado-md.md)方法打开[单元集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)对象， **ActiveConnection**属性将继承自变量的值。  
  
 设置**ActiveConnection**属性[目录](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)对象传递给**执行任何操作**释放关联的数据，包括中的数据[CubeDefs](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)集合和任何相关[维度](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)，[层次结构](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)，[级别](../../../ado/reference/ado-md-api/level-object-ado-md.md)，和[成员](../../../ado/reference/ado-md-api/member-object-ado-md.md)对象。 关闭**连接**用于打开对象**目录**具有相同的效果与设置**ActiveConnection**属性**执行任何操作**.  
  
 更改由所引用的连接的默认数据库**ActiveConnection**属性**目录**对象失效的内容**目录**。  
  
 如果你尝试更改将会出错**ActiveConnection**已打开的属性**单元集**对象。  
  
> [!NOTE]
>  在 Visual Basic 中，请记得使用**设置**关键字设置时**ActiveConnection**属性**连接**对象。 如果省略**设置**关键字，你将实际设置**ActiveConnection**属性等于**连接**对象的默认属性， **ConnectionString**。 这些代码将正常工作;但是，你将创建数据源，这可能造成负面性能影响的其他连接。  
  
 当使用 MSOLAP 数据访问接口，在服务器名称的连接字符串中设置数据源，并从数据源设置为目录的名称的初始目录。 若要连接到多维数据集文件从服务器断开连接，请将位置设置为的完整路径。CUB 文件。 在任一情况下，将设置为提供程序名称的提供程序。 例如，以下字符串使用 MSOLAP 访问接口连接到名为服务器上名为 Bobs 视频应用商店目录**Servername**:  
  
```  
"Data Source=Servername;Initial Catalog=Bobs Video Store;Provider=msolap"  
```  
  
 以下字符串连接到位置 C:\MSDASDK\samples\oledb\olap\data\bobsvid.cub 的本地多维数据集文件：  
  
```  
"Location=C:\MSDASDK\samples\oledb\olap\data\bobsvid.cub;Provider=msolap"  
```  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[目录对象 (ADO MD)](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)|[单元集对象 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)|  
  
## <a name="see-also"></a>另请参阅  
 [单元集示例 (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Open 方法 (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)
