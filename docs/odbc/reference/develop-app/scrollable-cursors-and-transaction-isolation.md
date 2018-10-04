---
title: 可滚动游标和事务隔离 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e5510eb58315f70195eb40390edec1766c350fb6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47662345"
---
# <a name="scrollable-cursors-and-transaction-isolation"></a>可滚动游标和事务隔离
下表列出了用于管理更改的可见性的因素。  
  
|所做的更改：|可见性取决于：|  
|----------------------|----------------------------|  
|游标|游标类型，游标实现|  
|同一个事务中的其他语句|游标类型|  
|在其他事务中的语句|游标类型，事务隔离级别|  
  
 这些因素在下图中显示。  
  
 ![控制更改可见性因素](../../../odbc/reference/develop-app/media/pr23.gif "pr23")  
  
 下表总结了每种游标类型能够检测所本身、 其自己的事务中的其他操作和其他事务所做的更改。 后一种更改的可见性取决于游标类型和包含光标的事务的隔离级别。  
  
|游标 type\action|自己|拥有<br /><br /> Txn|其他<br /><br /> Txn<br /><br /> (RU[a])|其他<br /><br /> Txn<br /><br /> (RC[a])|其他<br /><br /> Txn<br /><br /> (RR[a])|其他<br /><br /> Txn<br /><br /> (S[a])|  
|-------------------------|----------|-----------------|----------------------------------|----------------------------------|----------------------------------|---------------------------------|  
|静态|||||||  
|Insert|可以在 [b]|否|否|否|否|否|  
|Update|可以在 [b]|否|否|否|否|否|  
|DELETE|可以在 [b]|否|否|否|否|否|  
|键集驱动|||||||  
|Insert|可以在 [b]|否|否|否|否|否|  
|Update|用户帐户控制|是|是|是|否|否|  
|DELETE|可以在 [b]|用户帐户控制|是|是|否|否|  
|Dynamic|||||||  
|Insert|用户帐户控制|是|是|是|是|否|  
|Update|用户帐户控制|是|是|是|否|否|  
|DELETE|用户帐户控制|是|是|是|否|否|  
  
 [a] 中括号的字母指示包含游标的事务的隔离级别（在其中进行了更改） 的其他事务的隔离级别是不相关。  
  
 RU： 未提交的读  
  
 RC： 已提交读  
  
 RR： 可重复读  
  
 S： 可序列化  
  
 [b] 依赖于如何实现游标。 光标是否可以检测此类更改通过中的 SQL_STATIC_SENSITIVITY 选项将报告**SQLGetInfo**。
