---
title: "定义筛选器 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.replconflictviewer.definefilters.f1
helpviewer_keywords:
- Define Filters dialog box
ms.assetid: 1fa71d22-ce5a-4aae-ba05-4d755842aeac
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c1db30c8f31236cf3a106abd230f29454361ce43
ms.lasthandoff: 04/11/2017

---
# <a name="define-filters"></a>定义筛选器
  可以使用 **“定义筛选器”** 对话框定义筛选器，然后将筛选器应用于数据冲突以在网格中查看冲突的子集。 若要定义筛选器，请从 **“运算符”** 下拉列表框中选择运算符，然后输入值。 例如，若要只显示冲突解决落选方为服务器 **ReplTest1**的那些冲突，请从 **“运算符”** 下拉列表框中选择 **“等于”** ，然后在第一个 **“值”** 列中输入 **ReplTest1** 。  
  
## <a name="options"></a>选项  
 **“运算符”**  
 为筛选器选择一个运算符，例如 **“小于或等于”**。  
  
 **ReplTest1**  
 为筛选器输入一个值。 大多数运算符只需要在第一个 **“值”** 列中输入值，但 **“介于”** 和 **“不介于”** 运算符需要在两个 **“值”** 列中都输入值。  
  
 **Clear**  
 单击此按钮可以清除先前定义的所有筛选器。  
  
## <a name="see-also"></a>另请参阅  
 [Microsoft 复制冲突查看器（合并复制）](../../relational-databases/replication/microsoft-replication-conflict-viewer-merge-replication.md)   
 [Microsoft 复制冲突查看器（事务复制）](../../relational-databases/replication/microsoft-replication-conflict-viewer-transactional-replication.md)  
  
  
