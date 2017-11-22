---
title: "LocalDBShareInstance 函数 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: localdb
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: LocalDBShareInstance
apilocation: sqluserinstance.dll
apitype: DLLExport
ms.assetid: 21eb3b9a-7d32-455b-89bb-f624198cd202
caps.latest.revision: "9"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ed067918464c9a9b97c6e2e6a6d1d0a8bd2f9072
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="localdbshareinstance-function"></a>LocalDBShareInstance 函数
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]与其他计算机的用户，使用指定的共享的名称共享指定的 SQL Server Express LocalDB 实例。  
  
 **标头文件：** sqlncli.h  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT LocalDBShareInstance(  
           PSID pOwnerSID,  
           PCWSTR pInstancePrivateName,  
           PCWSTR pInstanceSharedName,   
           DWORD dwFlags   
);  
```  
  
## <a name="parameters"></a>Parameters  
 *pOwnerSID*  
 [输入] 实例所有者的 SID。  
  
 *pInstancePrivateName*  
 [输入] 要共享的 LocalDB 实例的专用名称。  
  
 *pInstanceSharedName*  
 [输入] 要共享的 LocalDB 实例的共享名称。  
  
 *dwFlags*  
 [输入] 保留供将来使用。 当前应设置为 0。  
  
## <a name="returns"></a>返回  
 S_OK  
 函数成功。  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../../relational-databases/express-localdb-error-messages/localdb-error-not-installed.md)  
 计算机上没有安装 SQL Server Express LocalDB。  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../../relational-databases/express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 一个或多个指定的输入参数无效。  
  
 [LOCALDB_ERROR_INVALID_INSTANCE_NAME](../../relational-databases/express-localdb-error-messages/localdb-error-invalid-instance-name.md)  
 指定的实例名称无效。  
  
 [LOCALDB_ERROR_UNKNOWN_INSTANCE](../../relational-databases/express-localdb-error-messages/localdb-error-unknown-instance.md)  
 指定的实例不存在。  
  
 [LOCALDB_ERROR_ADMIN_RIGHTS_REQUIRED](../../relational-databases/express-localdb-error-messages/localdb-error-admin-rights-required.md)  
 执行此操作需要管理员权限。  
  
 [LOCALDB_ERROR_SHARED_NAME_TAKEN](../../relational-databases/express-localdb-error-messages/localdb-error-shared-name-taken.md)  
 指定的共享名称名已存在。  
  
 [LOCALDB_ERROR_INSTANCE_ALREADY_SHARED](../../relational-databases/express-localdb-error-messages/localdb-error-instance-already-shared.md)  
 指定的实例已经共享。  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../../relational-databases/express-localdb-error-messages/localdb-error-internal-error.md)  
 发生了意外错误。 有关详细信息，请参阅事件日志。  
  
## <a name="remarks"></a>注释  
 使用 LocalDB API 的代码示例，请参阅[SQL Server Express LocalDB 参考](../../relational-databases/sql-server-express-localdb-reference.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Express LocalDB 标头信息和版本信息](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
  
  
