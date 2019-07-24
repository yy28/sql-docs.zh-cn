---
title: ICommandWithParameters |Microsoft Docs
description: ICommandWithParameters 接口
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 205a93fe5ce57a8b4c10fffb8648a1ef4c7b6506
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015458"
---
# <a name="icommandwithparameters"></a>ICommandWithParameters
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  数据库引擎[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]中的改进, 以允许 ICommandWithParameters:: GetParameterInfo 获取预期结果的更准确说明。 这些更准确的结果可能与以前版本[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中的 CommandWithParameters:: GetParameterInfo 返回的值不同。 有关详细信息, 请参阅[元数据发现](../../oledb/features/metadata-discovery.md)。  
  
 同样从 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 开始，在调用 ICommandWithParameters::SetParameterInfo 时，传递给 pwszName 参数的值必须是有效的标识符  。 有关详细信息，请参阅 [Database Identifiers](../../../relational-databases/databases/database-identifiers.md)。  
  
## <a name="see-also"></a>另请参阅  
 [接口&#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md) 
  
  
