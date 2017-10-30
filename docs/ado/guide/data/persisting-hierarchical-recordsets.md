---
title: "保留的分层记录集 |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- hierarchical Recordsets [ADO], persisting
- persisting hierarchical Recordsets [ADO]
- data shaping [ADO], hierarchical Recordsets
ms.assetid: 43798bb5-98a6-4ad6-9bf8-78154b3a1827
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a1c4a4fc782bfa6c6130a1acbd45ab1aa2ae3fcd
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="persisting-hierarchical-recordsets"></a>持久化分层记录集
你可以保存分层结构**记录集**到通过调用 ADTG 或 XML 格式的文件中[保存](../../../ado/reference/ado-api/save-method.md)方法。 但是，两个限制适用保存分层时**记录集**以 XML 格式的 s： 如果无法将它们以 xml 格式保存分层**记录集**包含挂起的更新，且不能保存参数化分层**记录集**。  
  
 有关数据调整的提供程序的详细信息，请参阅[用于 OLE DB 的 Microsoft 数据调整服务](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)(ADO) 和[OLE DB 数据调整服务概述](http://msdn.microsoft.com/en-us/9f51e471-8e85-448e-9fb8-b64bbf767bf3)。  
  
## <a name="see-also"></a>另请参阅  
 [调整示例数据](../../../ado/guide/data/data-shaping-example.md)   
 [正式形状语法](../../../ado/guide/data/formal-shape-grammar.md)   
 [在常规的形状命令](../../../ado/guide/data/shape-commands-in-general.md)

