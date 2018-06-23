---
title: FILESTREAM 支持 (OLE DB) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB [FILESTREAM support]
- FILESTREAM [SQL Server], OLE DB
ms.assetid: c2bd3dfd-6103-43d1-859e-8ed8d19c58d3
caps.latest.revision: 13
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ba270b26a5a290f5b5c6fdd2830f10b9bf695037
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017071"
---
# <a name="filestream-support-ole-db"></a>FILESTREAM 支持 (OLE DB)
  开头[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]和[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 10.0、 OLE DB 支持增强的 FILESTREAM 功能。 有关此功能的详细信息，请参阅[FILESTREAM 支持](../features/filestream-support.md)。 有关示例，请参阅[Filestream 和 OLE DB](../../native-client-ole-db-how-to/filestream/filestream-and-ole-db.md)。  
  
 为了发送和接收大于 2 GB 的 `varbinary(max)` 值，应用程序在参数和结果绑定中使用 `DBTYPE_IUNKNOWN`。 参数的提供程序必须调用 iunknown:: Queryinterface ISequentialStream 和返回 ISequentialStream 的结果。  
  
 用于 OLE DB，检查相关为 ISequentialStream 值将通过放宽。 当*wType*是`DBTYPE_IUNKNOWN`中`DBBINDING`结构，检查长度可以是禁用通过省略`DBPART_LENGTH`从*dwPart*或通过设置数据的长度 （按的偏移量*obLength*数据缓冲区中) 到 ~ 0。 在此情况下，提供程序将不检查值的长度，并且将请求和返回可通过流提供的所有数据。 这一更改将适用于所有大型对象 (LOB) 类型和 XML，但只在连接到 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]（或更高版本）服务器时才适用。 这将为开发人员提供更高的灵活性，同时为现有应用程序和下级服务器维护一致性和向下兼容性。  
  
 此更改影响所有传输数据，主要 irowset:: Getdata、 ICommand::Execute 和 IRowsetFastLoad::InsertRow 的接口。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Native Client 编程](../sql-server-native-client-programming.md)  
  
  