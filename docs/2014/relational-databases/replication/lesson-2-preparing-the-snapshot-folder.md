---
title: 第 2 课：准备快照文件夹 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: f286cde9-c0d0-43ef-b7ba-53c3cbb8906c
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: d15b08a5ff98392961c3f4fb01c397f220303e86
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/18/2018
ms.locfileid: "53591021"
---
# <a name="lesson-2-preparing-the-snapshot-folder"></a>第 2 课：准备快照文件夹
  在本课中，将学习如何配置用于创建和存储发布快照的快照文件夹。  
  
### <a name="to-create-a-share-for-the-snapshot-folder-and-assign-permissions"></a>为快照文件夹创建共享并分配权限  
  
1.  在 Windows 资源管理器中，定位到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据文件夹。 默认位置为 C:\Program Files\Microsoft SQL Server\MSSQL.X\MSSQL\Data。  
  
2.  创建名为 **repldata** 的新文件夹。  
  
3.  右键单击此文件夹，然后单击“属性”。  
  
4.  在“repldata 属性”对话框的“共享”选项卡上，单击“共享”。  
  
5.  在“文件共享”对话框中，单击“共享”，再单击“完成”。  
  
6.  在 **“安全性”** 选项卡上，单击 **“编辑”**。  
  
7.  在“权限”对话框中，单击“添加”。 在“选择用户、计算机、服务帐户或组”文本框中，键入在第 1 课中创建的快照代理帐户的名称，例如 \<_Machine_Name>_**\repl_snapshot**，其中 \<*Machine_Name>* 是发布服务器的名称。 单击“检查名称”，然后单击“确定”。  
  
8.  重复上一步为分发代理和合并代理添加权限，其格式分别为 \<_Machine_Name>_**\repl_distribution** 和 \<_Machine_Name>_**\repl_merge**。  
  
9. 验证是否允许以下权限：  
  
    -   repl_snapshot - 完全控制  
  
    -   repl_distribution - 读取  
  
    -   repl_merge - 读取  
  
10. 单击“确定”关闭“repldata 属性”对话框，并创建 repldata 共享。  
  
## <a name="next-steps"></a>后续步骤  
 您已经成功为快照文件夹配置了共享。 接下来，您将配置分发。 请参阅[第 3 课：配置分发](lesson-3-configuring-distribution.md)。  
  
## <a name="see-also"></a>请参阅  
 [保护快照文件夹的安全](security/secure-the-snapshot-folder.md)  
  
  
