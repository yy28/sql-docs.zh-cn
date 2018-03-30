---
title: ICommand (OLE DB) |Microsoft 文档
description: ICommand 接口 (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ICommand [OLE DB Driver for SQL Server]
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8ef3dda040713e2f5de4db81684317dbf0a42175
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2018
---
# <a name="icommand-ole-db"></a>ICommand (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本文讨论特定于 OLE DB 驱动程序的 SQL Server 的 OLE DB 行为。  
  
## <a name="icommandexecute"></a>ICommand::Execute  
 如果插入的数据大于列的大小，通常会导致错误。 但是，在一些情况下返回 S_OK 但*dwStatus*将设置为 DBSTATUS_S_TRUNCATED。 它通常发生在插入数据使用的参数，其中的列不是足够大以保存数据，和**ICommandWithParameters::SetParameterInfo**尚未调用。  
  
## <a name="see-also"></a>另请参阅  
 [接口 &#40; OLE DB &#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)
  
  
