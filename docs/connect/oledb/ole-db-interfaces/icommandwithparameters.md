---
title: ICommandWithParameters（OLE DB 驱动程序）| Microsoft Docs
description: 了解改进功能如何允许 ICommandWithParameters::GetParameterInfo 获取关于 OLE DB Driver for SQL Server 预期结果的更准确描述。
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 21f3643737d1d6682133a252d52a072f73e81dfb
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88861370"
---
# <a name="icommandwithparameters"></a>ICommandWithParameters
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  从 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 开始，数据库引擎中的改进功能允许 ICommandWithParameters::GetParameterInfo 获取关于预期结果的更准确描述。 这些更准确的结果可能与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以前版本中的 CommandWithParameters::GetParameterInfo 所返回的值有所不同。 有关详细信息，请参阅[元数据发现](../../oledb/features/metadata-discovery.md)。  
  
 同样从 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 开始，在调用 ICommandWithParameters::SetParameterInfo 时，传递给 pwszName 参数的值必须是有效的标识符  。 有关详细信息，请参阅 [Database Identifiers](../../../relational-databases/databases/database-identifiers.md)。  
  
## <a name="see-also"></a>另请参阅  
 [接口 (OLE DB)](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md) 
  
  
