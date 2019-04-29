---
title: MSSQLSERVER_41325 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 41325 (Database Engine error)
ms.assetid: 97c6a8bb-139a-44f3-9ed5-f46d047e8ed3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5c78044f8790f3a1ab97d036467813efa3d30e6b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62913993"
---
# <a name="mssqlserver41325"></a>MSSQLSERVER_41325
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件 ID|41325|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|HK_TX_COMMIT_SR_VALIDATION|  
|消息正文|因某个序列化读取验证失败，当前事务无法提交。|  
  
## <a name="explanation"></a>解释  
 事务遇到验证错误，已失败。  
  
## <a name="user-action"></a>用户操作  
 重试失败的事务。 有关详细信息，请参阅[内存中 OLTP&#40;内存中优化&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
  
## <a name="see-also"></a>请参阅  
 [内存中 OLTP（内存中优化）](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
