---
title: 关于 OLE DB 属性 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, properties
- SQL Server Native Client OLE DB provider, properties
- properties [OLE DB]
- property values [SQL Server Native Client]
ms.assetid: 0b36a61e-b542-400d-a3d2-e6f643caf2c6
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 81a928d788c3461a6f24baa46906d5af40a4e7ba
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37432636"
---
# <a name="about-ole-db-properties"></a>关于 OLE DB 属性
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  使用者设置属性值以请求特定的对象行为。 例如，使用者使用属性以指定要由行集公开的接口。 使用者获得属性值，以确定对象（比如行集、会话或数据源对象）的功能。  
  
 每个属性都有值、类型、说明和读/写属性，对于行集属性，还有一个用于指示是否可以逐列应用它的指示器。  
  
 属性由一个 GUID 和一个表示属性 ID 的整数进行标识。 属性集是所有具有相同 GUID 的一组属性。 除了预定义的 OLE DB 属性设置，则[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序中实现特定于提供程序的属性集和属性。 每个属性属于一个或多个属性组。 属性组是应用于特定对象的所有属性所形成的组。 属性组包括初始化属性组、数据源属性组、会话属性组、行集属性组、表属性组和列属性组等等。 在每个这样的属性组中都有属性。  
  
 设置属性值涉及：  
  
1.  确定要设置值的属性。  
  
2.  确定包含所标识属性的属性集。  
  
3.  分配 DBPROPSET 结构数组，每个标识的属性集一个。  
  
4.  为每个属性集分配 DBPROP 结构数组。 每个数组中的元素个数是属于该属性集的属性（在步骤 1 中标识）的个数。  
  
5.  填充每个属性的 DBPROP 结构。  
  
6.  在每个属性集的 DBPROPSET 结构中，填充信息（属性集 GUID、元素的计数以及对应的 DBPROP 数组的指针）。  
  
7.  调用方法以设置属性，并传递 DBPROPSET 结构的计数和数组。  
  
## <a name="see-also"></a>请参阅  
 [创建 SQL Server Native Client OLE DB 提供程序应用程序](../../relational-databases/native-client-ole-db-provider/creating-a-sql-server-native-client-ole-db-provider-application.md)   
 [属性 (OLE DB)](http://go.microsoft.com/fwlink/?LinkId=112207)  
  
  
