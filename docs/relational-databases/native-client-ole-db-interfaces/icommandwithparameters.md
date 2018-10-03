---
title: ICommandWithParameters |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 66644c70-def7-46d8-8c47-b883292a0288
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9414ce51d81ac826f017da4f000d5c83401bcaad
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47706505"
---
# <a name="icommandwithparameters"></a>ICommandWithParameters
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  以开头的数据库引擎中的改进[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]允许 icommandwithparameters:: Getparameterinfo 若要获取的预期的结果更准确描述。 这些更准确的结果可能不同于 CommandWithParameters::GetParameterInfo 的早期版本中返回的值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关详细信息，请参阅[元数据发现](../../relational-databases/native-client/features/metadata-discovery.md)。  
  
 同样从 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 开始，在调用 ICommandWithParameters::SetParameterInfo 时，传递给 pwszName 参数的值必须是有效的标识符。 有关详细信息，请参阅 [Database Identifiers](../../relational-databases/databases/database-identifiers.md)。  
  
## <a name="see-also"></a>请参阅  
 [接口&#40;OLE DB&#41;](http://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)  
  
  
