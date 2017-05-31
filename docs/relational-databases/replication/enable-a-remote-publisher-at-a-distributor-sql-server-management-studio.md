---
title: "在分发服务器上启用远程发布服务器 (SQL Server Management Studio) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- remote Distributors [SQL Server replication]
- Publishers [SQL Server replication]
ms.assetid: 6f8e2831-5c45-4e39-8e51-d37e2813cf3d
caps.latest.revision: 30
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 848c1142c1db178efe9215db06fd326ea4aade6e
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="enable-a-remote-publisher-at-a-distributor-sql-server-management-studio"></a>在分发服务器上启用远程发布服务器 (SQL Server Management Studio)
  可以在 **“发布服务器”** 页上允许发布服务器使用远程分发服务器。 可以在配置分发向导中通过“分发服务器属性 - \<分发服务器>”对话框访问此页。 有关使用该向导和访问该对话框的详细信息，请参阅[配置发布和分发](../../relational-databases/replication/configure-publishing-and-distribution.md)和[查看和修改分发服务器和发布服务器属性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)。  
  
### <a name="to-enable-a-publisher-in-the-configure-distribution-wizard"></a>在配置分发向导中启用发布服务器  
  
1.  在“配置分发向导”的 **“发布服务器”** 页上单击 **“添加”**。  
  
2.  单击 **“添加 SQL Server 发布服务器”**。 有关启用 Oracle 发布服务器以使用分发服务器的信息，请参阅 [Create a Publication from an Oracle Database](../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)。  
  
3.  在 **“连接到服务器”** 对话框中，指定要使用远程分发服务器的发布服务器的连接信息，再单击 **“连接”**。  
  
4.  在 **“分发服务器密码”** 页的 **“密码”** 和 **“确认密码”** 文本框中，为 **distributor_admin** 帐户指定强密码，复制将使用该密码从发布服务器连接到分发服务器以执行管理任务。  
  
5.  若要查看并修改发布服务器的设置，请单击属性按钮 (**...**)。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-enable-a-publisher-in-the-distributor-properties-dialog-box"></a>在“分发服务器属性”对话框中启用发布服务器  
  
1.  在“分发服务器属性 - \<分发服务器>”对话框的“发布服务器”页上，单击“添加”。  
  
2.  单击 **“添加 SQL Server 发布服务器”**。 有关启用 Oracle 发布服务器以使用分发服务器的信息，请参阅 [Create a Publication from an Oracle Database](../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)。  
  
3.  在 **“连接到服务器”** 对话框中，指定要使用远程分发服务器的发布服务器的连接信息，再单击 **“连接”**。  
  
4.  在 **“分发服务器”** 页的 **“密码”** 和 **“确认密码”** 文本框中，为 **distributor_admin** 帐户指定强密码，复制将使用该密码从发布服务器连接到分发服务器以执行管理任务。  
  
5.  若要查看并修改发布服务器的设置，请单击属性按钮 (**...**)。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [配置发布和分发](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [“配置分发”](../../relational-databases/replication/configure-distribution.md)   
 [保护分发服务器](../../relational-databases/replication/security/secure-the-distributor.md)  
  
  
