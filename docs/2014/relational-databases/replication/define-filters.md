---
title: 定义筛选器 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.rep.replconflictviewer.definefilters.f1
helpviewer_keywords:
- Define Filters dialog box
ms.assetid: 1fa71d22-ce5a-4aae-ba05-4d755842aeac
caps.latest.revision: 17
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: ae4d16f7b9f4cfaedb95e651ff4bb3c579d564c5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017307"
---
# <a name="define-filters"></a>定义筛选器
  可以使用 **“定义筛选器”** 对话框定义筛选器，然后将筛选器应用于数据冲突以在网格中查看冲突的子集。 若要定义筛选器，请从 **“运算符”** 下拉列表框中选择运算符，然后输入值。 例如，若要只显示冲突解决落选方为服务器 **ReplTest1**的那些冲突，请从 **“运算符”** 下拉列表框中选择 **“等于”** ，然后在第一个 **“值”** 列中输入 **ReplTest1** 。  
  
## <a name="options"></a>“常规”  
 **“运算符”**  
 为筛选器选择一个运算符，例如 **“小于或等于”**。  
  
 **ReplTest1**  
 为筛选器输入一个值。 大多数运算符只需要在第一个 **“值”** 列中输入值，但 **“介于”** 和 **“不介于”** 运算符需要在两个 **“值”** 列中都输入值。  
  
 **Clear**  
 单击此按钮可以清除先前定义的所有筛选器。  
  
## <a name="see-also"></a>请参阅  
 [Microsoft 复制冲突查看器（合并复制）](microsoft-replication-conflict-viewer-merge-replication.md)   
 [Microsoft 复制冲突查看器（事务复制）](microsoft-replication-conflict-viewer-transactional-replication.md)  
  
  