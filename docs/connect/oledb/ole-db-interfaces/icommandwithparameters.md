---
title: ICommandWithParameters |Microsoft Docs
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
ms.author: pelopes
manager: craigg
ms.openlocfilehash: ea2a3882a6f5b781df2ac42431d990e3ee1037f5
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43026646"
---
# <a name="icommandwithparameters"></a>ICommandWithParameters
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  以开头的数据库引擎中的改进[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]允许 icommandwithparameters:: Getparameterinfo 若要获取的预期的结果更准确描述。 这些更准确的结果可能不同于 CommandWithParameters::GetParameterInfo 的早期版本中返回的值[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 有关详细信息，请参阅[元数据发现](../../oledb/features/metadata-discovery.md)。  
  
 同样从 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 开始，在调用 ICommandWithParameters::SetParameterInfo 时，传递给 pwszName 参数的值必须是有效的标识符。 有关详细信息，请参阅 [Database Identifiers](../../../relational-databases/databases/database-identifiers.md)。  
  
## <a name="see-also"></a>另请参阅  
 [接口&#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md) 
  
  
