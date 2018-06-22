---
title: ICommandWithParameters |Microsoft 文档
description: ICommandWithParameters 接口
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: c41a3885293493299f6234f3dcc0ef5edc4040be
ms.sourcegitcommit: 03ba89937daeab08aa410eb03a52f1e0d212b44f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/16/2018
ms.locfileid: "35689110"
---
# <a name="icommandwithparameters"></a>ICommandWithParameters
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  以开头的数据库引擎中的改进[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]允许 ICommandWithParameters::GetParameterInfo 以获取更准确的预期结果的说明。 这些更准确的结果可能与在以前版本的 CommandWithParameters::GetParameterInfo 返回的值不同[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 有关详细信息，请参阅[元数据发现](../../oledb/features/metadata-discovery.md)。  
  
 此外从[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]，当调用 ICommandWithParameters::SetParameterInfo，传递给值*pwszName*参数必须是有效的标识符。 有关详细信息，请参阅 [Database Identifiers](../../../relational-databases/databases/database-identifiers.md)。  
  
## <a name="see-also"></a>请参阅  
 [接口&#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md) 
  
  
