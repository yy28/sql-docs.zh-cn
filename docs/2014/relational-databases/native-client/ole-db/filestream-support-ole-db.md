---
title: FILESTREAM 支持 (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB [FILESTREAM support]
- FILESTREAM [SQL Server], OLE DB
ms.assetid: c2bd3dfd-6103-43d1-859e-8ed8d19c58d3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ad6aa7b55906e68dba6615140ef2c6afcc3efaa5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62668930"
---
# <a name="filestream-support-ole-db"></a>FILESTREAM 支持 (OLE DB)
  开头[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]和[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 10.0，OLE DB 支持增强的 FILESTREAM 功能。 有关此功能的详细信息，请参阅[FILESTREAM 支持](../features/filestream-support.md)。 有关示例，请参阅[Filestream 和 OLE DB](../../native-client-ole-db-how-to/filestream/filestream-and-ole-db.md)。  
  
 为了发送和接收大于 2 GB 的 `varbinary(max)` 值，应用程序在参数和结果绑定中使用 `DBTYPE_IUNKNOWN`。 为参数提供程序必须调用 iunknown:: Queryinterface ISequentialStream 和 ISequentialStream 返回的结果。  
  
 对于 OLE DB，检查与 ISequentialStream 值相关的发布将放宽。 当*wType*是`DBTYPE_IUNKNOWN`中`DBBINDING`长度检查可以是结构，禁用通过省略`DBPART_LENGTH`从*dwPart*或通过设置数据的长度 （按的偏移量*obLength*数据缓冲区中) 为 ~ 0。 在此情况下，提供程序将不检查值的长度，并且将请求和返回可通过流提供的所有数据。 这一更改将适用于所有大型对象 (LOB) 类型和 XML，但只在连接到 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]（或更高版本）服务器时才适用。 这将为开发人员提供更高的灵活性，同时为现有应用程序和下级服务器维护一致性和向下兼容性。  
  
 此更改会影响所有传输的数据，主要 irowset:: Getdata、 icommand:: Execute 和 irowsetfastload:: Insertrow 的接口。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Native Client 编程](../sql-server-native-client-programming.md)  
  
  
