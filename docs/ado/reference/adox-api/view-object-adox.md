---
title: 查看对象 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- View
helpviewer_keywords:
- View object [ADOX]
ms.assetid: 653421ce-7b94-43d0-9bc6-4900f8f2af45
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6bc26e8d59c29bd7b1b0fbdd0a3a4fdb39f8fee1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67964849"
---
# <a name="view-object-adox"></a>视图对象 (ADOX)
表示一组筛选的记录或一个虚拟表。 与 ADO 一起使用时[命令](../../../ado/reference/ado-api/command-object-ado.md)对象，**视图**对象可以用于添加、 删除或修改视图。  
  
## <a name="remarks"></a>备注  
 视图是从其他数据库表或视图创建一个虚拟表。 **视图**对象使用户可以创建一个视图，而无需知道，或使用提供程序的"创建视图"语法。  
  
 使用的属性**视图**对象，你可以：  
  
-   指定与视图[名称](../../../ado/reference/adox-api/name-property-adox.md)属性。  
  
-   指定 ADO**命令**对象，它可用于添加、 删除或修改与视图[命令](../../../ado/reference/adox-api/command-property-adox.md)属性。  
  
-   返回日期信息与[DateCreated](../../../ado/reference/adox-api/datecreated-property-adox.md)并[DateModified](../../../ado/reference/adox-api/datemodified-property-adox.md)属性。  
  
 本部分包含以下主题。  
  
-   [视图对象属性、方法和事件](../../../ado/reference/adox-api/view-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>请参阅  
 [视图和字段集合示例 (VB)](../../../ado/reference/adox-api/views-and-fields-collections-example-vb.md)   
 [视图 Append 方法示例 (VB)](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [视图集合、 CommandText 属性示例 (VB)](../../../ado/reference/adox-api/views-collection-commandtext-property-example-vb.md)   
 [视图 Delete 方法示例 (VB)](../../../ado/reference/adox-api/views-delete-method-example-vb.md)   
 [视图集合 (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
