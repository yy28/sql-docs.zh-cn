---
title: "sysssislog (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysdtslog90_TSQL
- sysdtslog90
dev_langs:
- TSQL
helpviewer_keywords:
- sysssislog system table
ms.assetid: 7fa288a1-81e3-42a0-82f6-8a59019693d0
caps.latest.revision: 
author: spelluru
ms.author: spelluru
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 479c6158f7c26cde133fae66164dda89b9a39888
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="sysssislog-transact-sql"></a>sysssislog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包或其任务和容器在运行时生成的每个日志记录条目各占一行。 在安装 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 时，将在 msdb 数据库中创建该表。 如果将日志记录配置为记录到不同的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库，则会在指定的数据库中创建采用此格式的 sysssislog 表。  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 此表中写入日志记录条目**仅**当包使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]日志提供程序。  
  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|id|**int**|日志记录项的唯一标识符。|  
|事件|**sysname**|生成日志记录项的事件的名称。|  
|computer|**nvarchar**|生成日志记录条目时运行包的计算机。|  
|运算符后的表达式|**nvarchar**|运行生成日志记录条目的包的用户的名称。|  
|源 (source)|**nvarchar**|包中生成日志记录条目的可执行文件的名称。|  
|sourceid|**uniqueidentifier**|包中生成日志记录条目的可执行文件的 GUID。|  
|executionid|**uniqueidentifier**|生成日志记录条目的可执行文件的执行实例的 GUID。|  
|starttime|**datetime**|包开始运行的时间。|  
|endtime|**datetime**|包的完成时间。<br /><br /> 此功能尚未实现。 endtime 列中的值始终与 starttime 列中的值相同。|  
|datacode|**int**|一个可选的整数值，它通常表示运行容器或任务的结果。|  
|databytes|**image**|包含附加信息的可选字节数组。|  
|message|**nvarchar**|事件以及与事件关联的信息的说明。|  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services &#40;SSIS &#41;日志记录](../../integration-services/performance/integration-services-ssis-logging.md)   
  
  
