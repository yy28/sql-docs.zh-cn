---
title: MSSQLSERVER_125 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- "125"
helpviewer_keywords:
- 125 (Database Engine error)
ms.assetid: 0f58338d-2ea0-48b8-8a20-c438b0940433
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 59c732d80ccfafc8f242bb1c42fe60e3dea81f19
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84947777"
---
# <a name="mssqlserver_125"></a>MSSQLSERVER_125
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|125|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称||  
|消息正文|Case 表达式只能嵌套到 %d 层。|  
  
## <a name="explanation"></a>说明  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 仅允许在 CASE 表达式中嵌套 10 个级别。  
  
## <a name="user-action"></a>用户操作  
 将 CASE 语句的级别减少到 10 级或更低的级数。  
  
## <a name="see-also"></a>另请参阅  
 [CASE (Transact-SQL)](/sql/t-sql/language-elements/case-transact-sql)  
  
  
