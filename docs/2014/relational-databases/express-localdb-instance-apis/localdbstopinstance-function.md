---
title: LocalDBStopInstance 函数 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
api_name:
- LocalDBStopInstance
api_location:
- sqluserinstance.dll
topic_type:
- apiref
ms.assetid: 4bd73187-0aac-4f03-ac54-2b78e41917e5
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 6f28abbf9871d5f4e512e9c9ee0cfb5c7ad9db59
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63135248"
---
# <a name="localdbstopinstance-function"></a>LocalDBStopInstance 函数
  停止运行指定的 SQL Server Express LocalD 实例。  
  
 **头文件：** sqlncli.msi  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT LocalDBStopInstance(  
           PCWSTR pInstanceName,  
           DWORD dwFlags,   
           ULONG ulTimeout   
);  
```  
  
## <a name="parameters"></a>parameters  
 *pInstanceName*  
 [输入] 要停止的 LocalDB 实例的名称。  
  
 *dwFlags*  
 [输入] 指定要停止该实例的方法的一个标志或标志组合。  
  
 可用标志：  
  
 LOCALDB_SHUTDOWN_KILL_PROCESS  
 使用终止进程操作系统命令立即关闭。  
  
 LOCALDB_SHUTDOWN_WITH_NOWAIT  
 使用 Transact-SQL 命令 WITH NOWAIT 选项关闭。  
  
 如果没有设置标志，则使用 Transact-SQL 命令 SHUTDOWN 关闭 LocalDB 实例。 如果同时设置了这两个标志，则优先使用 LOCALDB_SHUTDOWN_KILL_PROCESS 标志。  
  
 *ulTimeout*  
 [输入] 等待此操作完成的时间（秒）。 如果该值为 0，此函数将立即返回，而不等待 LocalDB 实例停止。  
  
## <a name="returns"></a>返回  
 S_OK  
 函数成功。  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../express-localdb-error-messages/localdb-error-not-installed.md)  
 计算机上没有安装 SQL Server Express LocalDB。  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 一个或多个指定的输入参数无效。  
  
 [LOCALDB_ERROR_INVALID_INSTANCE_NAME](../express-localdb-error-messages/localdb-error-invalid-instance-name.md)  
 指定的实例名称无效。  
  
 [LOCALDB_ERROR_UNKNOWN_INSTANCE](../express-localdb-error-messages/localdb-error-unknown-instance.md)  
 该实例不存在。  
  
 [LOCALDB_ERROR_WAIT_TIMEOUT](../express-localdb-error-messages/localdb-error-wait-timeout.md)  
 尝试获取同步锁定时超时。  
  
 [LOCALDB_ERROR_INSTANCE_STOP_FAILED](../express-localdb-error-messages/localdb-error-instance-stop-failed.md)  
 停止操作在给定的时间内未能完成。  
  
 [LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG](../express-localdb-error-messages/localdb-error-instance-folder-path-too-long.md)  
 应在其中存储该实例的路径的长度超过 MAX_PATH。  
  
 [LOCALDB_ERROR_CANNOT_GET_USER_PROFILE_FOLDER](../express-localdb-error-messages/localdb-error-cannot-get-user-profile-folder.md)  
 无法检索用户配置文件的文件夹。  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_FOLDER](../express-localdb-error-messages/localdb-error-cannot-access-instance-folder.md)  
 无法访问实例文件夹。  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_REGISTRY](../express-localdb-error-messages/localdb-error-cannot-access-instance-registry.md)  
 无法访问实例注册表。  
  
 [LOCALDB_ERROR_INSTANCE_CONFIGURATION_CORRUPT](../express-localdb-error-messages/localdb-error-instance-configuration-corrupt.md)  
 实例配置已损坏。  
  
 [LOCALDB_ERROR_CALLER_IS_NOT_OWNER](../express-localdb-error-messages/localdb-error-caller-is-not-owner.md)  
 API 调用方不是 LocalDB 实例所有者。  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../express-localdb-error-messages/localdb-error-internal-error.md)  
 发生了意外错误。 有关详细信息，请参阅事件日志。  
  
## <a name="remarks"></a>备注  
 有关使用 LocalDB API 的代码示例，请参阅[SQL Server Express LocalDB 引用](../sql-server-express-localdb-reference.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Express LocalDB 标头信息和版本信息](sql-server-express-localdb-header-and-version-information.md)  
  
  
