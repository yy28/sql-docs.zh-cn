---
title: "catalog.create_customized_logging_level |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 20b3ba0a-126f-49bf-b70f-61b2a0fcb750
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 126fa0af811033bb0be035b1f4c550620c696bb3
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="catalogcreatecustomizedlogginglevel"></a>catalog.create_customized_logging_level
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  创建一个新的自定义日志记录级别。 有关自定义日志记录级别的详细信息，请参阅[Integration Services &#40;SSIS &#41;日志记录](../../integration-services/performance/integration-services-ssis-logging.md)。  
  
## <a name="syntax"></a>语法  
  
```sql  
create_customized_logging_level [ @level_name = ] level_name  
    , [ @level_description = ] level_description  
    , [ @profile_value = ] profile_value  
    , [ @event_value = ] event_value  
    , [ @level_id = ] level_id OUT  
  
```  
  
## <a name="arguments"></a>参数  
 [ @level_name =] *level_name*  
 对新的现有名称的自定义日志记录级别。  
  
 *Level_name*是**nvarchar （128)**。  
  
 [ @level_description =] *level_description*  
 新的现有的说明自定义日志记录级别。  
  
 *Level_description*是**nvarchar(1024)**。  
  
 [ @profile_value =] *profile_value*  
 所需新的统计信息的自定义日志记录级别来记录。  
  
 统计信息的有效值包括以下。 这些值对应的值上**统计信息**选项卡**自定义日志记录级别管理**对话框。  
  
-   执行 = 0  
  
-   卷 = 1  
  
-   性能 = 2  
  
 *Profile_value*是**bigint**。  
  
 [ @event_value =] *event_value*  
 你希望新事件的自定义日志记录级别来记录。  
  
 事件的有效值包括以下。 这些值对应的值上**事件**选项卡**自定义日志记录级别管理**对话框。  
  
|没有事件上下文的事件|事件的事件上下文|  
|----------------------------------|-------------------------------|  
|OnVariableValueChanged = 0<br /><br /> OnExecutionStatusChanged = 1<br /><br /> OnPreExecute = 2<br /><br /> OnPostExecute = 3<br /><br /> OnPreValidate = 4<br /><br /> OnPostValidate = 5<br /><br /> OnWarning = 6<br /><br /> OnInformation = 7<br /><br /> OnError = 8<br /><br /> OnTaskFailed = 9<br /><br /> OnProgress = 10<br /><br /> OnQueryCancel = 11<br /><br /> OnBreakpointHit = 12<br /><br /> OnCustomEvent = 13<br /><br /> 诊断 = 14<br /><br /> DiagnosticEx = 15<br /><br /> NonDiagnostic = 16|OnVariableValueChanged_IncludeContext = 32<br /><br /> OnExecutionStatusChanged_IncludeContext = 33<br /><br /> OnPreExecute_IncludeContext = 34<br /><br /> OnPostExecute_IncludeContext = 35<br /><br /> OnPreValidate_IncludeContext = 36<br /><br /> OnPostValidate_IncludeContext = 37<br /><br /> OnWarning_IncludeContext = 38<br /><br /> OnInformation_IncludeContext = 39<br /><br /> OnError_IncludeContext = 40<br /><br /> OnTaskFailed_IncludeContext = 41<br /><br /> OnProgress_IncludeContext = 42<br /><br /> OnQueryCancel_IncludeContext = 43<br /><br /> OnBreakpointHit_IncludeContext = 44<br /><br /> OnCustomEvent_IncludeContext = 45<br /><br /> Diagnostic_IncludeContext = 46<br /><br /> DiagnosticEx_IncludeContext = 47<br /><br /> NonDiagnostic_IncludeContext = 48|  
  
 *Event_value*是**bigint**。  
  
 [ @level_id =] *level_id*出  
 新的 id 的自定义日志记录级别。  
  
 *Level_id*是**bigint**。  
  
## <a name="remarks"></a>注释  
 若要合并多个值的 TRANSACT-SQL for *profile_value*或*event_value*自变量，执行此示例。 若要捕获 OnError (8) 和 DiagnosticEx (15) 事件，用于计算*event_value*是`2^8 + 2^15 = 33024`。  
  
## <a name="return-codes"></a>返回代码  
 0（成功）  
  
 存储过程失败时引发错误。  
  
## <a name="result-set"></a>结果集  
 无  
  
## <a name="permissions"></a>Permissions  
 此存储过程需要下列权限之一：  
  
-   **ssis_admin** 数据库角色中的成员资格  
  
-   **sysadmin** 服务器角色中的成员资格  
  
## <a name="errors-and-warnings"></a>错误和警告  
 下表说明了导致存储过程失败的情况。  
  
-   用户没有所需的权限。  
  
  
