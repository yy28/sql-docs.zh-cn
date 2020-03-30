---
title: MSSQLSERVER_10532 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10532 (Database Engine error)
ms.assetid: 01da29ee-bf67-433f-8148-587a7e8d1d76
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 050f1c4e1c47458e513e02d16eb3ea6dc7e842a8
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "72005985"
---
# <a name="mssqlserver_10532"></a>MSSQLSERVER_10532
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|10532|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|PG_NO_ELIGIBLE_STMT|  
|消息正文|无法创建计划指南“%.\*ls”，因为 **plan_handle 指定的批或模块不包含可用于计划指南的语句\@** 。 请为 **plan_handle 指定其他值\@** 。|  
  
## <a name="explanation"></a>说明  
由  **指定的批或模块不包含可用于计划指南的语句\@** 。  
  
## <a name="user-action"></a>用户操作  
请为 **plan_handle 指定其他值\@** 。  
  
## <a name="see-also"></a>另请参阅  
[计划指南](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide (Transact-SQL)](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[sp_create_plan_guide_from_handle (Transact-SQL)](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
