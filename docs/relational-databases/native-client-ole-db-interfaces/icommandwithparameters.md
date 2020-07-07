---
title: ICommandWithParameters | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 66644c70-def7-46d8-8c47-b883292a0288
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 454e155144f79ace30eb1e15048df7c30b293607
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86008380"
---
# <a name="icommandwithparameters"></a>ICommandWithParameters
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  从 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 开始，数据库引擎中的改进功能允许 ICommandWithParameters::GetParameterInfo 获取关于预期结果的更准确描述。 这些更准确的结果可能与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以前版本中的 CommandWithParameters::GetParameterInfo 所返回的值有所不同。 有关详细信息，请参阅[元数据发现](../../relational-databases/native-client/features/metadata-discovery.md)。  
  
 同样从 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 开始，在调用 ICommandWithParameters::SetParameterInfo 时，传递给 pwszName 参数的值必须是有效的标识符**。 有关详细信息，请参阅 [Database Identifiers](../../relational-databases/databases/database-identifiers.md)。  
  
## <a name="see-also"></a>另请参阅  
 [接口 &#40;OLE DB&#41;](https://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)  
  
  
