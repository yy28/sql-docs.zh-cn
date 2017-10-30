---
title: "保留的筛选和分层记录集 |Microsoft 文档"
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
- filtered Recordset persistence [ADO]
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: d01aeb4d-4e43-450b-b3f2-0c27eaaf9f86
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8de12620e57fe9cf7235c2a1f5a1442b429197d0
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="persisting-filtered-and-hierarchical-recordsets"></a>持久化筛选和分层记录集
如果[筛选器](../../../ado/reference/ado-api/filter-property.md)属性实际上是为**记录集**，保存筛选器访问的行。 如果**记录集**是分层的当前子**记录集**和其子都得到保存，包括父**记录集**。 如果**保存**方法的子**记录集**是调用子及其所有子级都保存，但不是父。 有关层次结构的详细信息**记录集**，请参阅[数据成型](../../../ado/guide/data/data-shaping.md)。  
  
> [!NOTE]
>  保存层次结构时存在一些限制**记录集**（数据形状） 以 XML 格式。 有关详细信息，请参阅[保留的记录，采用 XML 格式](../../../ado/guide/data/persisting-records-in-xml-format.md)。

