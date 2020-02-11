---
title: FILESTREAM 支持（OLE DB） |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62668930"
---
# <a name="filestream-support-ole-db"></a>FILESTREAM 支持 (OLE DB)
  从[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]和[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 开始，OLE DB 支持增强的 FILESTREAM 功能。 有关此功能的详细信息，请参阅[FILESTREAM 支持](../features/filestream-support.md)。 有关示例，请参阅[Filestream 和 OLE DB](../../native-client-ole-db-how-to/filestream/filestream-and-ole-db.md)。  
  
 为了发送和接收大于 2 GB 的 `varbinary(max)` 值，应用程序在参数和结果绑定中使用 `DBTYPE_IUNKNOWN`。 对于参数，提供程序必须为 ISequentialStream 调用 IUnknown：： QueryInterface，并为返回 ISequentialStream 的结果调用。  
  
 对于 OLE DB，与 ISequentialStream 值相关的检查将被宽松。 当*wType* `DBTYPE_IUNKNOWN`在`DBBINDING`结构中时，可以通过从`DBPART_LENGTH` *dwPart*中省略或将数据的长度（在数据缓冲区中的偏移量*obLength* ）设置为 ~ 0 来禁用长度检查。 在此情况下，提供程序将不检查值的长度，并且将请求和返回可通过流提供的所有数据。 这一更改将适用于所有大型对象 (LOB) 类型和 XML，但只在连接到 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]（或更高版本）服务器时才适用。 这将为开发人员提供更高的灵活性，同时为现有应用程序和下级服务器维护一致性和向下兼容性。  
  
 此更改会影响传输数据的所有接口，主要 IRowset：：，ICommand：： Execute 和 IRowsetFastLoad：： InsertRow。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client 编程](../sql-server-native-client-programming.md)  
  
  
