---
title: 连接到服务器（“其他连接参数”页）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.connecttoserver.options.registeredservers.f1
ms.assetid: ba34b01a-6289-4eb8-8341-fa3d9ec87b3f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e92fbb8bc29aed54e43925a0670d9a365388df62
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62808668"
---
# <a name="connect-to-server-additional-connection-parameters-page"></a>连接到服务器（“其他连接参数”页）
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 的“连接到”对话框将最常用的连接字符串值作为选项提供。 使用“其他连接参数”页可以将更多连接参数添加到连接字符串。  
  
-   其他连接参数可以是任一 ODBC 连接参数。  
  
-   应以 **;parameter1=value1;parameter2=value2** 格式添加其他连接参数。  
  
-   使用“其他连接参数”页添加的参数添加到使用“连接到”对话框选项选择的参数中。  
  
-   所提供的各个参数的最后一个实例均覆盖该参数的任何以前的实例。 使用“其他连接参数”页添加的参数跟踪并替换“登录名”或“连接属性”选项卡中提供的参数。 例如，如果“登录名”选项卡给出的“服务器名称”为 **SERVER1**，而“其他连接参数”页包含 **;SERVER=SERVER2**，则会连接到 **SERVER2**。  
  
-   使用“其他连接参数”页添加的参数始终作为纯文本传递。  
  
    > [!IMPORTANT]  
    >  “其他连接参数”页中不可包括登录凭据和密码。 否则，它们将在没有加密的情况下通过网络传递。 请改用“登录名”选项卡。  
  
## <a name="task-list"></a>任务列表  
  
### <a name="to-show-the-additional-connection-parameters-page"></a>显示“其他连接参数”页  
  
1.  在 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 的“查询”菜单上指向“连接”，然后单击“连接”。  
  
2.  在“连接到”对话框中，单击“选项”，然后单击“其他连接参数”选项卡。  
  
## <a name="examples"></a>示例  
  
### <a name="example-a-connecting-to-the-database-engine"></a>示例 a:连接到数据库引擎  
 若要连接到名为 ACCOUNTING 的服务器上的 [!INCLUDE[ssSampleDBnormal](../includes/sssampledbnormal-md.md)] 数据库，请在“其他连接参数”页中输入以下内容：  
  
```  
;SERVER=ACCOUNTING;DATABASE=AdventureWorks2012  
```  
  
### <a name="example-b-connecting-to-analysis-services"></a>示例 b:连接到 Analysis Services  
 若要连接到 Analysis Server 并实时（跳过缓存）查询侦听通知的各部分，且将写回超时值设置为 5，则请在“其他连接参数”页中输入以下内容：  
  
```  
;Real Time Olap=TRUE;Writeback Timeout=5  
```  
  
  
