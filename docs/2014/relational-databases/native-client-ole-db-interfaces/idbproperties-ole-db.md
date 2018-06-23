---
title: IDBProperties (OLE DB) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 2e5a4fd8-5164-495a-9986-3477aef8d8a5
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 3bee573d18bce37685612ab79a715834ca27e5fe
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36028568"
---
# <a name="idbproperties-ole-db"></a>IDBProperties (OLE DB)
  OLE DB 标准规范允许提供程序为 `DBPROPINFO::vValues` 指定 VT_EMPTY。 但是， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 调用时始终返回 VT_EMPTY`IDBProperties::GetPropertyInfo`与`DBPROPSET_ROWSETALL`检索行集属性。  
  
## <a name="see-also"></a>请参阅  
 [接口&#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)  
  
  