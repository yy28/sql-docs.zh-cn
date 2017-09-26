---
title: "catalog.create_execution_dump |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 91319b0b-5536-4ab4-a403-9559ed9dd177
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b05e1b46845c0a2b5ee47b94dc239d79d4a12a17
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="catalogcreateexecutiondump"></a>catalog.create_execution_dump
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  导致暂停正在运行的包并创建转储文件。 文件存储在*\<驱动器 >*: files\microsoft SQL Server\130\Shared\ErrorDumps 文件夹。  
  
## <a name="syntax"></a>语法  
  
```tsql  
create_execution_dump [ @execution_id = ] execution_id  
  
```  
  
## <a name="arguments"></a>参数  
 [ @execution_id =] *execution_id*  
 正在运行的包的执行 ID。 *Execution_id*是**bigint**。  
  
## <a name="example"></a>示例  
 在以下示例中，系统提示将为正在运行的执行 ID 为 88 的包创建转储文件。  
  
```  
  
EXEC create_execution_dump @execution_id = 88  
  
```  
  
## <a name="return-codes"></a>返回代码  
 0（成功）  
  
 存储过程失败时引发错误。  
  
## <a name="result-set"></a>结果集  
 无  
  
## <a name="permissions"></a>Permissions  
 此存储的过程要求用户是的成员**ssis_admin**数据库角色。  
  
## <a name="errors-and-warnings"></a>错误和警告  
 下表说明了导致存储过程失败的情况。  
  
-   指定了无效的执行 ID。  
  
-   包已完成。  
  
-   包当前正在创建转储文件。  
  
## <a name="see-also"></a>另请参阅  
 [生成包执行的转储文件](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)  
  
  
