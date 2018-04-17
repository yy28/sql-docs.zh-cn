---
title: GetPathLocator (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- GetPathLocator
- GetPathLocator_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GetPathLocator function
ms.assetid: 78b7e220-445b-4fdf-811b-7253f4f2b058
caps.latest.revision: 15
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 15d4c04f98677d1e7749c2ee94b6410e2a845560
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="getpathlocator-transact-sql"></a>GetPathLocator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  返回 FileTable 中指定文件或目录的路径定位器 ID 值。  
  
## <a name="syntax"></a>语法  
  
```  
  
GetPathLocator(filenamespace_path)  
```  
  
## <a name="arguments"></a>参数  
 *filenamespace_path*  
 FileTable 中的命名空间路径。 命名空间路径属于类型**nvarchar (max)**。  
  
 如果数据库属于 Alwayson 可用性组，则**GetPathLocator**函数接受虚拟网络名称 (VNN) 或计算机名称。  
  
## <a name="return-type"></a>返回类型  
 **hierarchyid**  
  
## <a name="general-remarks"></a>一般备注  
 有关详细信息，请参阅 [Work with Directories and Paths in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)。  
  
## <a name="examples"></a>示例  
 你可以使用**GetPathLocator**函数时将文件从文件服务器迁移到 FileTable。 在这种情况下，您需要将文件移入 FileTable，然后用 FileTable UNC 路径替换每个文件的原始 UNC 路径。 有关完整示例，请参阅[文件加载到 Filetable](../../relational-databases/blob/load-files-into-filetables.md)。  
  
## <a name="see-also"></a>另请参阅  
 [在 FileTable 中使用目录和路径](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)  
  
  
