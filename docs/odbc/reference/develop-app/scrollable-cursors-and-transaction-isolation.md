---
title: 可滚动光标和事务隔离 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- isolation levels [ODBC]
- scrollable cursors [ODBC]
- transaction isolation [ODBC]
- transactions [ODBC], isolation
ms.assetid: f0216f4a-46e3-48ae-be0a-e2625e8403a6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7e40278bd209132736aee2788b5648ffa84a44e6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304218"
---
# <a name="scrollable-cursors-and-transaction-isolation"></a>可滚动游标和事务隔离
下表列出了管理更改可见性的因素。  
  
|所做的更改：|可见性取决于：|  
|----------------------|----------------------------|  
|游标|游标类型，游标实现|  
|同一事务中的其他语句|光标类型|  
|其他事务中的报表|游标类型、事务隔离级别|  
  
 这些因素如下图所示。  
  
 ![控制更改可见性的因素](../../../odbc/reference/develop-app/media/pr23.gif "pr23")  
  
 下表总结了每种游标类型检测自身、自身事务中的其他操作和其他事务所做的更改的能力。 后一个更改的可见性取决于游标类型和包含游标的事务的隔离级别。  
  
|光标类型\操作|自己|自己<br /><br /> Txn|Othr<br /><br /> Txn<br /><br /> （RU_a]）|Othr<br /><br /> Txn<br /><br /> （RC[a]）|Othr<br /><br /> Txn<br /><br /> （RR[a]）|Othr<br /><br /> Txn<br /><br /> （S[a]）|  
|-------------------------|----------|-----------------|----------------------------------|----------------------------------|----------------------------------|---------------------------------|  
|Static|||||||  
|插入|也许[b]|否|否|否|否|否|  
|更新|也许[b]|否|否|否|否|否|  
|删除|也许[b]|否|否|否|否|否|  
|键集驱动|||||||  
|插入|也许[b]|否|否|否|否|否|  
|更新|是|是|是|是|否|否|  
|删除|也许[b]|是|是|是|否|否|  
|动态|||||||  
|插入|是|是|是|是|是|否|  
|更新|是|是|是|是|否|否|  
|删除|是|是|是|是|否|否|  
  
 [a] 括号中的字母指示包含光标的事务的隔离级别;另一个事务的隔离级别（进行更改时）不相关。  
  
 RU：读取未提交  
  
 RC：读取已提交  
  
 RR：可重复读取  
  
 S： 可序列化  
  
 [b] 取决于光标的实现方式。 光标能否检测到此类更改是通过**SQLGetInfo**中的SQL_STATIC_SENSITIVITY选项报告的。
