---
description: LocalDBStartTracing 函数
title: LocalDBStartTracing 函数 |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
apiname:
- LocalDBStartTracing
apilocation:
- sqluserinstance.dll
apitype: DLLExport
ms.assetid: c7b83833-6d2a-4a06-9cb7-42767bed52c6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 854a840375601a6d571afa21b734cec6fb23b2b5
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542935"
---
# <a name="localdbstarttracing-function"></a>LocalDBStartTracing 函数
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  对当前 Windows 用户拥有的所有 SQL Server Express LocalDB 实例启用 API 调用跟踪。  
  
 **头文件：** sqlncli.msi  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT LocalDBStartTracing();  
```  
  
## <a name="returns"></a>返回  
 S_OK  
 函数成功。  
  
 [LOCALDB_ERROR_XEVENT_FAILED](../../relational-databases/express-localdb-error-messages/localdb-error-xevent-failed.md)  
 无法启动 LocalDB 实例 API 内的 XEvent 引擎。  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../../relational-databases/express-localdb-error-messages/localdb-error-internal-error.md)  
 发生了意外错误。 有关详细信息，请参阅事件日志。  
  
## <a name="remarks"></a>备注  
 有关使用 LocalDB API 的代码示例，请参阅 [SQL Server Express LocalDB 引用](../../relational-databases/sql-server-express-localdb-reference.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Express LocalDB 标头信息和版本信息](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
  
  
