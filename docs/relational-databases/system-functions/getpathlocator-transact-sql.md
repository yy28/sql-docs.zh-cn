---
title: GetPathLocator (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- GetPathLocator
- GetPathLocator_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GetPathLocator function
ms.assetid: 78b7e220-445b-4fdf-811b-7253f4f2b058
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 7770ced88953fd64d9ce48b624416b9a7e787f7e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47699125"
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
 FileTable 中的命名空间路径。 类型的命名空间路径是**nvarchar （max)**。  
  
 如果数据库所属的 Always On 可用性组，则**GetPathLocator**函数接受虚拟网络名称 (VNN) 或计算机名称。  
  
## <a name="return-type"></a>返回类型  
 **hierarchyid**  
  
## <a name="general-remarks"></a>一般备注  
 有关详细信息，请参阅 [Work with Directories and Paths in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)。  
  
## <a name="examples"></a>示例  
 可以使用**GetPathLocator**函数时将文件从文件服务器迁移到 FileTable。 在这种情况下，您需要将文件移入 FileTable，然后用 FileTable UNC 路径替换每个文件的原始 UNC 路径。 有关完整示例，请参阅[将文件加载到 Filetable](../../relational-databases/blob/load-files-into-filetables.md)。  
  
## <a name="see-also"></a>请参阅  
 [在 FileTable 中使用目录和路径](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)  
  
  
