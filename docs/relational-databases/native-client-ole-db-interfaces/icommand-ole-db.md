---
title: ICommand (OLE DB) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ICommand [SQL Server Native Client]
ms.assetid: 5e24b3a0-0658-44fc-b653-f4c52f9eb328
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 483c45ea2761a87e15a258ceca793dd09e1173f5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32945112"
---
# <a name="icommand-ole-db"></a>ICommand (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  本主题讨论特定于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 的 OLE DB 行为。  
  
## <a name="icommandexecute"></a>ICommand::Execute  
 如果插入的数据大于列的大小，通常会导致错误。 但是，在一些情况下返回 S_OK 但*dwStatus*将设置为 DBSTATUS_S_TRUNCATED。 这通常发生在时插入数据使用的参数，其中列是不足够大以保存数据，和**ICommandWithParameters::SetParameterInfo**尚未调用。  
  
## <a name="see-also"></a>另请参阅  
 [接口 & #40; OLE DB & #41;](http://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)  
  
  
