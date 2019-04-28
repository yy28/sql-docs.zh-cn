---
title: 这些策略导入到单个实例 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: bc5bcd87-663f-41d9-bb7b-b3e083cd63df
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 410f3a317a9d3ad2f8cab52d9f57fd4a63c1c36c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62865096"
---
# <a name="import-the-policies-to-a-single-instance"></a>将策略导入到单个实例
  在此任务中，您将要计划的最佳实践策略导入到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的单个实例上的基于策略的管理中。  
  
## <a name="prerequisites"></a>先决条件  
 您必须在运行 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 或更高版本的服务器上执行此过程。  
  
### <a name="import-the-best-practices-policies-for-the-database-engine"></a>为数据库引擎导入最佳实践策略  
  
1.  启动 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]，然后连接到[!INCLUDE[ssDE](../includes/ssde-md.md)]。  
  
2.  在对象资源管理器，展开**管理**，然后展开**策略管理**。  
  
3.  右键单击**策略**，然后单击**导入策略**。  
  
4.  在中**导入**对话框旁边**要导入文件**框中，单击省略号 (**...**) 按钮。  
  
5.  在中**查找**列表中，浏览到包含最佳实践策略的以下文件夹：  
  
     **C:\Program Files (x86)\Microsoft SQL Server\110\Tools\Policies\DatabaseEngine\1033**  
  
    > [!NOTE]  
    >  文件路径可能各不相同，具体取决于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 程序文件的安装位置、运行的操作系统是 32 位还是 64 位以及语言标识符。  
  
6.  在中**选择策略**对话框中，选择一个或多个策略文件。  
  
     若要选择多个不相邻的文件，请单击一个文件，按住 Ctrl 键，然后单击各个其他文件。 若要选择多个相邻的文件，请单击序列中的第一个文件，按住 Shift 键，然后单击最后一个文件。  
  
7.  完成选择文件后，单击**打开**。  
  
8.  在**导入**对话框框中，请确保**策略状态**列表设置为**保留导入时的策略状态**（默认值），然后单击**确定**.  
  
     策略导入**策略**节点下的**策略管理**。 默认情况下，导入的策略设置为“按需”评估模式。  
  
## <a name="next-steps"></a>后续步骤  
 [计划策略](../../2014/tutorials/schedule-the-policies.md)  
  
  
