---
title: catalog.rename_customized_logging_level | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: b1a57d5e-3f03-4901-8b2b-bb8b371b595b
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c4f7b74e7b496cd16f73e7976a1d108b26372bb3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47665315"
---
# <a name="catalogrenamecustomizedlogginglevel"></a>catalog.rename_customized_logging_level
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  重命名现有的自定义日志记录级别。 有关自定义日志记录级别的详细信息，请参阅 [Integration Services (SSIS) 日志记录](../../integration-services/performance/integration-services-ssis-logging.md)。  
  
## <a name="syntax"></a>语法  
  
```sql  
catalog.rename_customized_logging_level [ @old_name = ] old_name  
    , [ @new_name = ] new_name  
```  
  
## <a name="arguments"></a>参数  
 [ @old_name = ] old_name  
 要重命名的现有自定义日志记录级别的名称。  
  
 old_name 为 nvarchar(128)。  
  
 [ @new_name = ] new_name  
 指定的自定义日志记录级别的新名称。  
  
 new_name 为 nvarchar(128)。  
  
## <a name="remarks"></a>Remarks  
  
## <a name="return-codes"></a>返回代码  
 0（成功）  
  
 存储过程失败时引发错误。  
  
## <a name="result-set"></a>结果集  
 None  
  
## <a name="permissions"></a>Permissions  
 此存储过程需要下列权限之一：  
  
-   **ssis_admin** 数据库角色中的成员资格  
  
-   **sysadmin** 服务器角色中的成员资格  
  
## <a name="errors-and-warnings"></a>错误和警告  
 下表说明了导致存储过程失败的情况。  
  
-   用户不具有所需的权限。  
  
  
