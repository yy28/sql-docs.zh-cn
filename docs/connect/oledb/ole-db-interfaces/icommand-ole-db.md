---
title: ICommand (OLE DB) | Microsoft Docs
description: ICommand 接口 (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- ICommand [OLE DB Driver for SQL Server]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 722536a086abf280cacded3ecd2cd0d450a417ae
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67994488"
---
# <a name="icommand-ole-db"></a>ICommand (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  本文介绍特定于 OLE DB Driver for SQL Server 的 OLE DB 行为。  
  
## <a name="icommandexecute"></a>ICommand::Execute  
 如果插入的数据大于列的大小，通常会导致错误。 但是，可能会出现将返回 S_OK、但 dwStatus 将设置为 DBSTATUS_S_TRUNCATED 的情况  。 这通常在插入带有参数的数据时发生，其中列的大小不足以容纳数据，并且尚未调用 ICommandWithParameters::SetParameterInfo  。  
  
## <a name="see-also"></a>另请参阅  
 [接口 (OLE DB)](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)
  
  
