---
title: "调整用于 OLE DB （ADO 服务提供程序） 的服务的 Microsoft 数据 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- providers [ADO], data shaping service for OLE DB
- data shaping service for OLE DB [ADO]
ms.assetid: 523009ce-e01b-4e2d-a7df-816d7688aff0
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3510664e97b64c36b7c1c7b42ca475194b6d01e2
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="microsoft-data-shaping-service-for-ole-db-overview"></a>Microsoft 数据定形 OLE DB 概述的服务
> [!IMPORTANT]
>  将 Windows 的未来版本中删除该功能。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，应用程序应使用 XML。

 Microsoft 数据调整服务 OLE DB 服务提供程序支持的分层构造 （形状）[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)从数据提供程序的对象。

## <a name="provider-keyword"></a>提供程序关键字
 若要对于 OLE DB 调用数据调整服务，请在连接字符串中指定以下关键字和值。

```
"Provider=MSDataShape"
```

## <a name="dynamic-properties"></a>动态属性
 当调用此服务提供程序时，将下面的动态属性添加到[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象。

|动态属性名称|Description|
|---------------------------|-----------------|
|**唯一的形状名称**|指示是否**记录集**具有重复值的对象及其**重新调整形状名称**允许属性。 如果此动态属性为**True**和新**记录集**创建具有相同的用户指定形状名称与现有**记录集**，然后新**记录集**修改对象的形状名称以确保其唯一性。 如果此属性为**False**和新**记录集**创建具有相同的用户指定形状名称与现有**记录集**，这两个**记录集**对象将具有相同的调整形状名称。 因此，既不**记录集**，只要两个记录集存在可以改变。<br /><br /> 属性的默认值是**False**。|
|**数据提供程序**|指示将提供要定形的行的提供程序的名称。 如果提供程序不会用于提供行，此值可以为 NONE。|

 此外可以通过指定其名称作为连接字符串中的关键字设置可写的动态属性。 例如，在 Microsoft Visual Basic 中，设置**数据提供程序**动态属性通过指定"MSDASQL":

```
Dim cn as New ADODB.Connection
cn.Open "Provider=MSDataShape;Data Provider=MSDASQL"
```

 你还可以设置或通过指定其名称作为到索引中检索的动态属性[属性](../../../ado/reference/ado-api/properties-collection-ado.md)属性。 例如，下面的代码示例获取在指定的位置，并输出的当前值**数据提供程序**动态属性，然后设置新的值，如果 cn。DataProvider 已设置为"MSDataShape"(直接或间接通过连接字符串) 和未打开连接：

```
Debug.Print cn.Properties("Data Provider")
cn.Properties("Data Provider") = "MSDASQL"
```

> [!NOTE]
>  动态属性，**数据提供程序**，可以是一组仅在未打开**连接**对象。 打开连接时，一旦**数据提供程序**属性变为只读的。

 有关数据调整的详细信息，请参阅[数据成型](../../../ado/guide/data/data-shaping-overview.md)。

## <a name="see-also"></a>另请参阅
 [附录 a： 提供程序](../../../ado/guide/appendixes/appendix-a-providers.md)

