---
title: catalog.create_execution_dump | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 91319b0b-5536-4ab4-a403-9559ed9dd177
caps.latest.revision: "12"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e8fc97f65fb17605393505c428b645994d3fd1da
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="catalogcreateexecutiondump"></a>catalog.create_execution_dump
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  导致暂停正在运行的包并创建转储文件。 此文件存储在 \<drive>:\Program Files\Microsoft SQL Server\130\Shared\ErrorDumps文件夹中。  
  
## <a name="syntax"></a>语法  
  
```sql  
catalog.create_execution_dump [ @execution_id = ] execution_id  
  
```  
  
## <a name="arguments"></a>参数  
 [ @execution_id = ] execution_id  
 正在运行的包的执行 ID。 execution_id 为 bigint。  
  
## <a name="example"></a>示例  
 在以下示例中，系统提示将为正在运行的执行 ID 为 88 的包创建转储文件。  
  
```sql
EXEC create_execution_dump @execution_id = 88  
```  
  
## <a name="return-codes"></a>返回代码  
 0（成功）  
  
 存储过程失败时引发错误。  
  
## <a name="result-set"></a>结果集  
 无  
  
## <a name="permissions"></a>Permissions  
 此存储过程要求用户为具有 ssis_admin 数据库角色的成员。  
  
## <a name="errors-and-warnings"></a>错误和警告  
 下表说明了导致存储过程失败的情况。  
  
-   指定了无效的执行 ID。  
  
-   包已完成。  
  
-   包当前正在创建转储文件。  
  
## <a name="see-also"></a>另请参阅  
 [生成包执行的转储文件](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)  
  
  
