---
title: "LocalDBStopTracing 函数 |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: localdb
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- LocalDBStopTracing
apilocation:
- sqluserinstance.dll
apitype: DLLExport
ms.assetid: 1d50e040-8602-4ffa-be8f-b8633fdfa7ff
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3c588e0be321f576d4d45fc3c659c34ef09da2d8
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/19/2018
---
# <a name="localdbstoptracing-function"></a>LocalDBStopTracing 函数
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  对当前 Windows 用户拥有的所有 SQL Server Express LocalDB 实例禁用 API 调用跟踪。  
  
 **标头文件：** sqlncli.h  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT LocalDBStopTracing();  
```  
  
## <a name="returns"></a>返回  
 S_OK  
 函数成功。  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../../relational-databases/express-localdb-error-messages/localdb-error-internal-error.md)  
 发生了意外错误。 有关详细信息，请参阅事件日志。  
  
## <a name="remarks"></a>注释  
 使用 LocalDB API 的代码示例，请参阅[SQL Server Express LocalDB 参考](../../relational-databases/sql-server-express-localdb-reference.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Express LocalDB 标头信息和版本信息](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
  
  
