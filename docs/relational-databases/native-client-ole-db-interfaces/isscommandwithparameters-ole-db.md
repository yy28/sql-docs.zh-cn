---
title: ISSCommandWithParameters (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSCommandWithParameters (OLE DB)
apitype: COM
helpviewer_keywords:
- ISSCommandWithParameters interface
ms.assetid: 3419b7f3-36a3-4863-816e-e641e4e90496
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 85f5ab9d465e20eb47265d06773b63728470603b
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2018
ms.locfileid: "39559577"
---
# <a name="isscommandwithparameters-ole-db"></a>ISSCommandWithParameters (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **ISSCommandWithParameters**公开支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]XML 和用户定义类型 (UDT)。 这是一个可选接口继承自核心 OLE DB 接口**ICommandWithParameters**。 除了三个方法继承自**ICommandWithParameters**;**GetParameterInfo**， **MapParameterNames**，并**SetParameterInfo**;**ISSCommandWithParameters**提供用于处理服务器特定的数据类型的两种新方法。  
  
> [!NOTE]  
>  **ISSCommandWithParameters**时使用服务组件，但是服务组件自身不会使用此接口，可以使用接口。  
  
|方法|Description|  
|------------|-----------------|  
|[Isscommandwithparameters:: Getparameterproperties &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-getparameterproperties-ole-db.md)|对传递到该命令的每个 UDT 或 XML 参数返回数组中的一个 SSPARAMPROPS 属性集结构，但是对于其他类型的参数，不会返回任何内容。|  
|[Isscommandwithparameters:: Setparameterproperties &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md)|按照序号基于每个参数设置参数属性，或者通过指定 SSPARAMPROPS 结构数组来设置大容量参数属性。|  
  
## <a name="see-also"></a>请参阅  
 [接口&#40;OLE DB&#41;](http://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)   
 [使用 XML 数据类型](../../relational-databases/native-client/features/using-xml-data-types.md)   
 [使用用户定义类型](../../relational-databases/native-client/features/using-user-defined-types.md)  
  
  
