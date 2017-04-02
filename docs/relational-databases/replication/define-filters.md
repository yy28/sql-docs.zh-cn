---
title: "定义筛选器 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.replconflictviewer.definefilters.f1"
helpviewer_keywords: 
  - "“定义筛选器”对话框"
ms.assetid: 1fa71d22-ce5a-4aae-ba05-4d755842aeac
caps.latest.revision: 18
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 18
---
# 定义筛选器
  可以使用 **“定义筛选器”** 对话框定义筛选器，然后将筛选器应用于数据冲突以在网格中查看冲突的子集。 若要定义筛选器，选择从一个运算符 **运算符** 下拉列表框中，然后输入一个值。 例如，若要显示在该冲突解决落选方是服务器这些冲突 **ReplTest1**, ，选择 **等于** 从 **运算符** 下拉列表框中，然后输入 **ReplTest1** 在第一个 **值** 列。  
  
## 选项  
 **运算符**  
 选择一个运算符的筛选器，如 **小于或等于**。  
  
 **值**  
 为筛选器输入一个值。 大多数运算符只需要在第一个 **“值”** 列中输入值，但 **“介于”** 和 **“不介于”** 运算符需要在两个 **“值”** 列中都输入值。  
  
 **Clear**  
 单击此按钮可以清除先前定义的所有筛选器。  
  
## 另请参阅  
 [Microsoft 复制冲突查看器 & #40;合并复制和 #41;](../../relational-databases/replication/microsoft-replication-conflict-viewer-merge-replication.md)   
 [Microsoft 复制冲突查看器 & #40;事务复制和 #41;](../../relational-databases/replication/microsoft-replication-conflict-viewer-transactional-replication.md)  
  
  