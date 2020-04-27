---
title: LocalDBStartInstance 函数 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
api_name:
- LocalDBStartInstance
api_location:
- sqluserinstance.dll
topic_type:
- apiref
ms.assetid: cb325f5d-10ee-4a56-ba28-db0074ab3926
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: ad86f5989fe9ff90132637d062b708423f23eef1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63131494"
---
# <a name="localdbstartinstance-function"></a>LocalDBStartInstance 函数
  启动指定的 SQL Server Express LocalDB 实例。  
  
 **头文件：** sqlncli.msi  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT LocalDBStartInstance(  
           PCWSTR pInstanceName,  
           DWORD dwFlags,   
           LPWSTR wszSqlConnection,   
           LPDWORD lpcchSqlConnection   
);  
```  
  
## <a name="parameters"></a>参数  
 *pInstanceName*  
 [输入] 要启动的 LocalDB 实例的名称。  
  
 dwFlags**  
 [输入] 保留供将来使用。 当前应设置为 0。  
  
 *wszSqlConnection*  
 [输出] 要存储 LocalDB 实例的连接字符串的缓冲区。  
  
 *lpcchSqlConnection*  
 [输入/输出]输入时包含*wszSqlConnection*缓冲区的大小（包括任何尾随 null）。 输出时，如果给定的缓冲区太小，则包含所需的缓冲区大小（以字符为单位），包括任何尾随空格。  
  
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
  
 [LOCALDB_ERROR_INSUFFICIENT_BUFFER](../express-localdb-error-messages/localdb-error-insufficient-buffer.md)  
 指定的缓冲区*wszSqlConnection*太小。  
  
 [LOCALDB_ERROR_WAIT_TIMEOUT](../express-localdb-error-messages/localdb-error-wait-timeout.md)  
 尝试获取同步锁定时超时。  
  
 [LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG](../express-localdb-error-messages/localdb-error-instance-folder-path-too-long.md)  
 应在其中存储该实例的路径的长度超过 MAX_PATH。  
  
 [LOCALDB_ERROR_CANNOT_GET_USER_PROFILE_FOLDER](../express-localdb-error-messages/localdb-error-cannot-get-user-profile-folder.md)  
 无法检索用户配置文件的文件夹。  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_FOLDER](../express-localdb-error-messages/localdb-error-cannot-access-instance-folder.md)  
 无法访问实例文件夹。  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_REGISTRY](../express-localdb-error-messages/localdb-error-cannot-access-instance-registry.md)  
 无法访问实例注册表。  
  
 [LOCALDB_ERROR_CANNOT_MODIFY_INSTANCE_REGISTRY](../express-localdb-error-messages/localdb-error-cannot-modify-instance-registry.md)  
 无法修改实例注册表。  
  
 [LOCALDB_ERROR_CANNOT_CREATE_SQL_PROCESS](../express-localdb-error-messages/localdb-error-cannot-create-sql-process.md)  
 无法创建 SQL Server 进程。  
  
 [LOCALDB_ERROR_SQL_SERVER_STARTUP_FAILED](../express-localdb-error-messages/localdb-error-sql-server-startup-failed.md)  
 SQL Server 进程已启动，但 SQL Server 启动失败。  
  
 [LOCALDB_ERROR_INSTANCE_CONFIGURATION_CORRUPT](../express-localdb-error-messages/localdb-error-instance-configuration-corrupt.md)  
 实例配置已损坏。  
  
 [LOCALDB_ERROR_AUTO_INSTANCE_CREATE_FAILED](../express-localdb-error-messages/localdb-error-auto-instance-create-failed.md)  
 不能创建自动实例。 有关错误详细信息，请参阅 Windows 应用程序事件日志。  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../express-localdb-error-messages/localdb-error-internal-error.md)  
 发生了意外错误。 有关详细信息，请参阅事件日志。  
  
## <a name="details"></a>详细信息  
 连接缓冲区参数（*wszSqlConnection*）和连接缓冲区大小参数（*lpcchSqlConnection*）都是可选的。 下表显示了为使用这些参数提供的选项及其结果。  
  
|Buffer|缓冲区大小|理由|操作|  
|------------|-----------------|---------------|------------|  
|Null|Null|用户想要启动实例，而不需要管道名称。|启动实例（不返回管道且不要求返回缓冲区大小）。|  
|Null|现值|用户要求提供输出缓冲区大小。 （在下一次调用中，用户将可能要求实际启动。)|返回所需的缓冲区大小（不启动且不返回管道）。 结果为 S_OK。|  
|现值|Null|不允许；输入不正确。|返回结果为 LOCALDB_ERROR_INVALID_PARAMETER。|  
|现值|现值|用户想要启动实例，并且在启动后需要管道名称以便连接到此实例。|检查缓冲区大小，启动实例，并在缓冲区中返回管道名称。 <br />Buffer size 参数返回 "server =" 字符串的长度，不包括终止 null。|  
  
 有关使用 LocalDB API 的代码示例，请参阅[SQL Server Express LocalDB 引用](../sql-server-express-localdb-reference.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Express LocalDB 标头信息和版本信息](sql-server-express-localdb-header-and-version-information.md)  
  
  
