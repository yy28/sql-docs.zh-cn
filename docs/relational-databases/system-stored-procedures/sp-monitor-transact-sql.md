---
title: sp_monitor (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_monitor_TSQL
- sp_monitor
dev_langs:
- TSQL
helpviewer_keywords:
- sp_monitor
ms.assetid: cb628496-2f9b-40e4-b018-d0831c4cb018
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 277062160e01f0111eeade2dc4a05b3c6a3ab59d
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33259627"
---
# <a name="spmonitor-transact-sql"></a>sp_monitor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  显示有关的统计信息[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_monitor  
```  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名|Description|  
|-----------------|-----------------|  
|**last_run**|时间**sp_monitor**上次运行。|  
|**current_run**|时间**sp_monitor**正在运行。|  
|**seconds**|以来经过的秒数**sp_monitor**已运行。|  
|**cpu_busy**|服务器计算机的 CPU 处理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工作所用的秒数。|  
|**io_busy**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在输入和输出操作上花费的秒数。|  
|**空闲**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已空闲的秒数。|  
|**packets_received**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 读取的输入数据包数。|  
|**packets_sent**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已写入的输出数据包数。|  
|**packet_errors**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在读取和写入数据包时遇到的错误数。|  
|**total_read**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 读取的次数。|  
|**total_write**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 写入的次数。|  
|**total_errors**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在读取和写入时遇到的错误数。|  
|**连接**|登录或尝试登录 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的次数。|  
  
## <a name="remarks"></a>注释  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 通过一系列函数跟踪其完成的工作量。 执行**sp_monitor**显示这些函数返回的当前值并显示自上次运行该过程的时间后中已更改量。  
  
 为每个列统计信息打印窗体中*数*(*数*)-*数*%或*数*(*数*). 第一个*数*指的秒数 (为**cpu_busy**， **io_busy**，和**空闲**) 或 （对于其他总数变量） 因为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]已重新启动。 *数*在括号中引用的秒数或自从上次总数**sp_monitor**已运行。 百分比是时间的百分比**sp_monitor**上次运行。 例如，如果此报表显示**cpu_busy**作为 4250 （215)-68 %cpu 已忙 4250 后的秒数[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]向上 215 秒自上一次启动**sp_monitor**上次运行，并且有 68%的总时间**sp_monitor**上次运行。  
  
## <a name="permissions"></a>权限  
 要求具有 **sysadmin** 固定服务器角色的成员身份。  
  
## <a name="examples"></a>示例  
 下面的示例报告有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 繁忙程度的信息。  
  
```  
USE master  
EXEC sp_monitor  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
||||  
|-|-|-|  
|**last_run**|**current_run**|**seconds**|  
|Mar 29 1998 11:55AM|Apr 4 1998 2:22 PM|561|  
  
||||  
|-|-|-|  
|**cpu_busy**|**io_busy**|**空闲**|  
|190(0)-0%|187(0)-0%|148(556)-99%|  
  
||||  
|-|-|-|  
|**packets_received**|**packets_sent**|**packet_errors**|  
|16(1)|20(2)|0(0)|  
  
|||||  
|-|-|-|-|  
|**total_read**|**total_write**|**total_errors**|**连接**|  
|141(0)|54920(127)|0(0)|4(0)|  
  
## <a name="see-also"></a>另请参阅  
 [sp_who (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
