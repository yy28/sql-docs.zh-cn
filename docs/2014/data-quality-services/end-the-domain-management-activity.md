---
title: 结束域管理活动 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: ab6505ad-3090-453b-bb01-58435e7fa7c0
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 3d25d369870dc7a4f53e70a61726ffbb7d38d9f5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65480616"
---
# <a name="end-the-domain-management-activity"></a>结束域管理活动
  本主题介绍如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中完成、关闭或取消域管理活动。 由于向导不执行域管理，因此，可以从域管理活动的任意页面中使用下面描述的控件。  
  
## <a name="end-domain-management"></a>结束域管理  
 **“完成”**  
 单击可完成域管理。 将显示一个弹出窗口，支持您执行以下操作：  
  
-   **是 - 发布知识库并退出**：将发布该知识库供当前用户或其他人使用。 将不锁定该知识库，该知识库（在知识库表中）的状态将设置为空，且域管理和知识发现活动都将可用。 您将返回到“打开知识库”屏幕。  
  
-   **否 - 保存对知识库所做的工作并退出**：将保存你的工作，该知识库将保持锁定状态，且该知识库的状态将设置为“工作中”。 域管理和知识发现活动都将可用。 您将返回到主页。  
  
-   **取消 - 停留在当前屏幕上**：系统将关闭弹出窗口并将你转回“域管理”屏幕。  
  
 **取消**  
 单击可终止域管理活动，不保存所做的工作，并返回到 DQS 主页。  
  
 **关闭**  
 单击可保存所做的工作，并返回到 DQS 主页。 知识库将被锁定，且该知识库在 **“打开知识库”** 屏幕的知识库表中的状态将为 **“域管理”**。 单击 **“关闭”** 后，若要执行知识发现活动，您必须返回 **“域管理”** 屏幕，单击 **“完成”**，然后单击 **“是”** 发布该知识库，或单击 **“否”** 保存对该知识库所做的工作并退出。  有关打开锁定的知识库的详细信息，请参阅 [Open a Knowledge Base](../../2014/data-quality-services/open-a-knowledge-base.md)。  
  
  
