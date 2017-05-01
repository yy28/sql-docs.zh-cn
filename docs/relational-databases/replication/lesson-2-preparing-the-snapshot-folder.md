---
title: "第 2 课：准备快照文件夹 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: f286cde9-c0d0-43ef-b7ba-53c3cbb8906c
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f9b63fa28f53724adce16bedda14e11cd3a750b8
ms.lasthandoff: 04/11/2017

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
  
7.  在“权限”对话框中，单击“添加”。 在“选择用户、计算机、服务帐户或组”文本框中，键入在第 1 课中创建的快照代理帐户的名称，例如 \<*Machine_Name>***\repl_snapshot**，其中 \<*Machine_Name>* 是发布服务器的名称。 单击“检查名称”，然后单击“确定”。  
  
8.  重复上一步为分发代理和合并代理添加权限，其格式分别为 \<*Machine_Name>***\repl_distribution** 和 \<*Machine_Name>***\repl_merge**。  
  
9. 验证是否允许以下权限：  
  
    -   repl_snapshot - 完全控制  
  
    -   repl_distribution - 读取  
  
    -   repl_merge - 读取  
  
10. 单击“确定”关闭“repldata 属性”对话框，并创建 repldata 共享。  
  
## <a name="next-steps"></a>后续步骤  
您已经成功为快照文件夹配置了共享。 接下来，您将配置分发。 请参阅 [第 3 课：配置分发](../../relational-databases/replication/lesson-3-configuring-distribution.md)。  
  
## <a name="see-also"></a>另请参阅  
[保护快照文件夹的安全](../../relational-databases/replication/security/secure-the-snapshot-folder.md)  
  
  
  

