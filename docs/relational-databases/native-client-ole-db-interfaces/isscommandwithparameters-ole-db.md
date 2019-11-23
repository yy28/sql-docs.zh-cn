---
title: ISSCommandWithParameters （OLE DB） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- ISSCommandWithParameters (OLE DB)
apitype: COM
helpviewer_keywords:
- ISSCommandWithParameters interface
ms.assetid: 3419b7f3-36a3-4863-816e-e641e4e90496
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 08291b998c0f540b56cad59d29433135993487c8
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2019
ms.locfileid: "73761960"
---
# <a name="isscommandwithparameters-ole-db"></a>ISSCommandWithParameters (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **ISSCommandWithParameters**公开对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] XML 和用户定义类型（UDT）的支持。 这是一个可选接口，它继承自 core OLE DB interface **ICommandWithParameters**。 除了从**ICommandWithParameters**继承的三个方法;**GetParameterInfo**、 **MapParameterNames**和**SetParameterInfo**;**ISSCommandWithParameters**提供了两种新方法用于处理特定于服务器的数据类型。  
  
> [!NOTE]  
>  使用服务组件时，可以使用**ISSCommandWithParameters**接口，但服务组件本身将不会使用此接口。  
  
|方法|描述|  
|------------|-----------------|  
|[ISSCommandWithParameters::GetParameterProperties &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-getparameterproperties-ole-db.md)|对传递到该命令的每个 UDT 或 XML 参数返回数组中的一个 SSPARAMPROPS 属性集结构，但是对于其他类型的参数，不会返回任何内容。|  
|[ISSCommandWithParameters::SetParameterProperties &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md)|按照序号基于每个参数设置参数属性，或者通过指定 SSPARAMPROPS 结构数组来设置大容量参数属性。|  
  
## <a name="see-also"></a>另请参阅  
 [接口&#40;OLE DB&#41; ](https://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)   
 [使用 XML 数据类型](../../relational-databases/native-client/features/using-xml-data-types.md)   
 [使用用户定义类型](../../relational-databases/native-client/features/using-user-defined-types.md)  
  
  
