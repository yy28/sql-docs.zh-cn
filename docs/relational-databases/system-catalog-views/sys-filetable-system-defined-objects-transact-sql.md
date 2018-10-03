---
title: sys.filetable_system_defined_objects (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.filetable_system_defined_objects_TSQL
- filetable_system_defined_objects
- filetable_system_defined_objects_TSQL
- sys.filetable_system_defined_objects
dev_langs:
- TSQL
helpviewer_keywords:
- sys.filetable_system_defined_objects catalog view
ms.assetid: 62022e6b-46f6-495f-b14b-53f41e040361
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d18b3c20a78c4f819827a389a3811946bfef33ce
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47660755"
---
# <a name="sysfiletablesystemdefinedobjects-transact-sql"></a>sys.filetable_system_defined_objects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  显示与 FileTable 相关的系统定义对象的列表。 为每个系统定义对象包含一行。  
  
 创建 FileTable 时将同时创建相关的对象（如约束和索引）。 您不能更改或删除这些对象；仅当删除 FileTable 本身时，它们才消失。  
  
 有关 FileTable 的详细信息，请参阅 [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)。  
  
|“列”|数据类型|Description|  
|------------|---------------|-----------------|  
|**object_id**|**int**|与 FileTable 相关的系统定义对象的对象 ID。<br /><br /> 引用中的对象**sys.objects**。|  
|**parent_object_id**|**int**|父 FileTable 的对象 ID。<br /><br /> 引用中的对象**sys.objects**。|  
  
## <a name="see-also"></a>请参阅  
 [创建、更改和删除 FileTable](../../relational-databases/blob/create-alter-and-drop-filetables.md)   
 [管理 FileTable](../../relational-databases/blob/manage-filetables.md)  
  
  
