---
title: 控件更改到记录集基础表 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Unique Table property [ADO]
- Unique Schema property [ADO]
- Unique Catalog property [ADO]
ms.assetid: d0e775d8-e353-46a1-ad10-ed4cc240dfaa
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1b70920cd223223d5efb14925a6808168ca9cc16
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67911681"
---
# <a name="unique-table-unique-schema-unique-catalog-properties-dynamic-ado"></a>唯一表、 唯一架构，唯一目录属性-动态 (ADO)
使您能够密切控制修改为在特定的基表[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)的由多个基表上的联接操作。  
  
-   **唯一表**指定对其允许更新、 插入和删除操作的基础表的名称。  
  
-   **唯一的架构**指定*架构*，或表的所有者的名称。  
  
-   **唯一目录**指定*目录*，或包含表的数据库的名称。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**字符串**是表、 架构或目录的名称的值。  
  
## <a name="remarks"></a>备注  
 由其目录、 架构和表名称唯一标识所需的基本表。 当**唯一表**属性设置的值**唯一架构**或**唯一目录**属性用于查找基表。 预期的位置，但不是必需的一个或两**唯一架构**并**唯一目录**属性设置之前**唯一表**属性设置。  
  
 主键**唯一表**视为整个主键**记录集**。 这是需要的主键的任何方法使用的密钥。  
  
 虽然**唯一表**设置，则[删除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)方法影响仅命名的表。 [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)，[重新同步](../../../ado/reference/ado-api/resync-method.md)，[更新](../../../ado/reference/ado-api/update-method.md)，以及[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法会影响任何适当基础表的**记录集**。  
  
 **唯一表**执行任何自定义重新同步之前，必须指定。 如果**唯一表**未指定， [Resync Command](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)属性会产生任何效果。  
  
 如果找不到唯一的基表，将导致运行时错误。  
  
 这些动态属性被追加到**记录集**对象[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合时[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性设置为**adUseClient**。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
