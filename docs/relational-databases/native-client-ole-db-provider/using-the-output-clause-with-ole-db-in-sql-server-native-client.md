---
title: "使用 SQL Server 本机客户端中的 OLE DB 使用 OUTPUT 子句 |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-provider
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 53deeb99-c088-4fde-844b-b2d91d6de1eb
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 626c21e7f246b705b7b9a1b880cfb8e0ae434cfe
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="using-the-output-clause-with-ole-db-in-sql-server-native-client"></a>在 SQL Server Native Client 中对 OLE DB 使用 OUTPUT 子句
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  如果你在 INSERT、 UPDATE、 DELETE 中使用 OUTPUT 子句，或合并命令，受影响的行计数不可用。 应用程序必须进行计数 OUTPUT 子句返回的行集中的行的数。  
  
## <a name="see-also"></a>另请参阅  
 [创建 SQL Server Native Client OLE DB 提供程序应用程序](../../relational-databases/native-client-ole-db-provider/creating-a-sql-server-native-client-ole-db-provider-application.md)  
  
  
