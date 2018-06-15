---
title: 控件更改到记录集基表 (ADO) |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Unique Table property [ADO]
- Unique Schema property [ADO]
- Unique Catalog property [ADO]
ms.assetid: d0e775d8-e353-46a1-ad10-ed4cc240dfaa
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8351eb10101219b09450055526f0cb6a47a95b5f
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35282691"
---
# <a name="unique-table-unique-schema-unique-catalog-properties-dynamic-ado"></a>唯一表，唯一的架构，唯一目录属性的动态 (ADO)
使您能够紧密控制特定基础表中的修改[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)的组上多个基表的联接操作而形成。  
  
-   **唯一表**指定的更新、 插入和删除允许在其基础表的名称。  
  
-   **唯一架构**指定*架构*，或表的所有者的名称。  
  
-   **唯一的目录**指定*目录*，或包含表的数据库的名称。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**字符串**是表、 架构或目录的名称的值。  
  
## <a name="remarks"></a>Remarks  
 由其目录、 架构和表名称唯一标识所需的基表。 当**唯一表**设置属性，值**唯一架构**或**唯一目录**属性用于查找基表。 这是预期的位置，但不是必需的任一或全部**唯一架构**和**唯一目录**之前设置属性**唯一表**属性设置。  
  
 主键值**唯一表**视为整个的主键**记录集**。 这是可用于任何方法，该方法需要主密钥的密钥。  
  
 虽然**唯一表**设置，[删除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)方法影响仅命名的表。 [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)，[重新同步](../../../ado/reference/ado-api/resync-method.md)，[更新](../../../ado/reference/ado-api/update-method.md)，和[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法影响任何相应基础表的**记录集**。  
  
 **唯一表**执行任何自定义的重新同步之前，必须指定。 如果**唯一表**未指定，[重新同步命令](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)属性将产生任何影响。  
  
 如果找不到唯一的基表，将导致运行时错误。  
  
 这些动态属性将追加到**记录集**对象[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合时[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性设置为**adUseClient**。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
