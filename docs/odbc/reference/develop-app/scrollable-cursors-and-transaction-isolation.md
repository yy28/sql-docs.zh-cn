---
description: 可滚动游标和事务隔离
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 790b2d0c4d80c821645c3a4360d1295cc55a8a4e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476499"
---
# <a name="scrollable-cursors-and-transaction-isolation"></a>可滚动游标和事务隔离
下表列出了控制更改可见性的因素。  
  
|所做的更改：|可见性取决于：|  
|----------------------|----------------------------|  
|游标|游标类型，游标实现|  
|同一事务中的其他语句|游标类型|  
|其他事务中的语句|游标类型，事务隔离级别|  
  
 下图显示了这些因素。  
  
 ![控制更改可见性的因素](../../../odbc/reference/develop-app/media/pr23.gif "pr23")  
  
 下表总结了每个游标类型检测自身所做的更改的能力，以及由其自己的事务中的其他操作和其他事务。 后一种更改的可见性取决于游标类型和包含游标的事务的隔离级别。  
  
|Cursor type\action|自己|不同<br /><br /> Txn|其他<br /><br /> Txn<br /><br />  (RU [a] ) |其他<br /><br /> Txn<br /><br />  (RC [a] ) |其他<br /><br /> Txn<br /><br />  (RR [a] ) |其他<br /><br /> Txn<br /><br />  (S [a] ) |  
|-------------------------|----------|-----------------|----------------------------------|----------------------------------|----------------------------------|---------------------------------|  
|静态|||||||  
|插入|也许 [b]|否|否|否|否|否|  
|更新|也许 [b]|否|否|否|否|否|  
|删除|也许 [b]|否|否|否|否|否|  
|键集驱动|||||||  
|插入|也许 [b]|否|否|否|否|否|  
|更新|是|是|是|是|否|否|  
|删除|也许 [b]|是|是|是|否|否|  
|动态|||||||  
|插入|是|是|是|是|是|否|  
|更新|是|是|是|是|否|否|  
|删除|是|是|是|是|否|否|  
  
 [a] 括号中的字母指示包含游标的事务的隔离级别;在其中进行更改的其他事务 (的隔离级别是不相关的) 。  
  
 RU：未提交读  
  
 RC：已提交读  
  
 RR：可重复读  
  
 S： Serializable  
  
 [b] 依赖于如何实现游标。 光标是否可以检测到此类更改通过 **SQLGetInfo**中的 SQL_STATIC_SENSITIVITY 选项进行报告。
