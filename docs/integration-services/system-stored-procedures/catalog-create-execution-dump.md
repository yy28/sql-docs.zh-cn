---
title: catalog.create_execution_dump | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 91319b0b-5536-4ab4-a403-9559ed9dd177
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 901f430f09621c6ad9be20759cddb757e2e96ee7
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295507"
---
# <a name="catalogcreate_execution_dump"></a>catalog.create_execution_dump 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  导致暂停正在运行的包并创建转储文件。 此文件存储在 \<drive>:\Program Files\Microsoft SQL Server\130\Shared\ErrorDumps文件夹中  。  
  
## <a name="syntax"></a>语法  
  
```sql  
catalog.create_execution_dump [ @execution_id = ] execution_id  
  
```  
  
## <a name="arguments"></a>参数  
 [ @execution_id = ] execution_id   
 正在运行的包的执行 ID。 execution_id 为 bigint   。  
  
## <a name="example"></a>示例  
 在以下示例中，系统提示将为正在运行的执行 ID 为 88 的包创建转储文件。  
  
```sql
EXEC create_execution_dump @execution_id = 88  
```  
  
## <a name="return-codes"></a>返回代码  
 0（成功）  
  
 存储过程失败时引发错误。  
  
## <a name="result-set"></a>结果集  
 None  
  
## <a name="permissions"></a>权限  
 此存储过程要求用户为具有 ssis_admin 数据库角色的成员  。  
  
## <a name="errors-and-warnings"></a>错误和警告  
 下表说明了导致存储过程失败的情况。  
  
-   指定了无效的执行 ID。  
  
-   包已完成。  
  
-   包当前正在创建转储文件。  
  
## <a name="see-also"></a>另请参阅  
 [生成包执行的转储文件](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)  
  
  
