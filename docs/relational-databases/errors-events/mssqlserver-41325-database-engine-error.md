---
title: MSSQLSERVER_41325 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 41325 (Database Engine error)
ms.assetid: 97c6a8bb-139a-44f3-9ed5-f46d047e8ed3
caps.latest.revision: 7
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d80dac919dde0e3edc039479accadc39404b6ef9
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

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
重试失败的事务。 有关详细信息，请参阅[内存中 OLTP&#40;内存中优化&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
  
## <a name="see-also"></a>另请参阅  
[内存中 OLTP（内存中优化）](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  

