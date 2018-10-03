---
title: IDBProperties (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 2e5a4fd8-5164-495a-9986-3477aef8d8a5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3b6dada26e15fc83d890b270ad553eb051bb08fa
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48135867"
---
# <a name="idbproperties-ole-db"></a>IDBProperties (OLE DB)
  OLE DB 标准规范允许提供程序为 `DBPROPINFO::vValues` 指定 VT_EMPTY。 但是， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 调用时始终返回 VT_EMPTY`IDBProperties::GetPropertyInfo`与`DBPROPSET_ROWSETALL`来检索行集属性。  
  
## <a name="see-also"></a>请参阅  
 [接口&#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)  
  
  
