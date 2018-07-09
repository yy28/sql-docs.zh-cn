---
title: FILESTREAM 支持 (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: native-client-ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB [FILESTREAM support]
- FILESTREAM [SQL Server], OLE DB
ms.assetid: c2bd3dfd-6103-43d1-859e-8ed8d19c58d3
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ad287aad1d87310a93bb2917d889775bba1e0650
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37420006"
---
# <a name="filestream-support-ole-db"></a>FILESTREAM 支持 (OLE DB)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  开头[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]和[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 10.0，OLE DB 支持增强的 FILESTREAM 功能。 有关此功能的详细信息，请参阅[FILESTREAM 支持](../../../relational-databases/native-client/features/filestream-support.md)。 有关示例，请参阅[Filestream 和 OLE DB](../../../relational-databases/native-client-ole-db-how-to/filestream/filestream-and-ole-db.md)。  
  
 若要发送和接收**varbinary （max)** 大于 2 GB 的值，应用程序使用**DBTYPE_IUNKNOWN**参数和结果绑定中。 为参数提供程序必须调用 iunknown:: Queryinterface ISequentialStream 和 ISequentialStream 返回的结果。  
  
 对于 OLE DB，检查与 ISequentialStream 值相关的发布将放宽。 当*wType*是**DBTYPE_IUNKNOWN**中**DBBINDING**结构，检查长度可以是禁用通过省略**DBPART_LENGTH**从*dwPart*或通过设置数据的长度 (偏移量位置处*obLength*数据缓冲区中) 为 ~ 0。 在此情况下，提供程序将不检查值的长度，并且将请求和返回可通过流提供的所有数据。 这一更改将适用于所有大型对象 (LOB) 类型和 XML，但只在连接到 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]（或更高版本）服务器时才适用。 这将为开发人员提供更高的灵活性，同时为现有应用程序和下级服务器维护一致性和向下兼容性。  
  
 此更改会影响所有传输的数据，主要 irowset:: Getdata、 icommand:: Execute 和 irowsetfastload:: Insertrow 的接口。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Native Client 编程](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
