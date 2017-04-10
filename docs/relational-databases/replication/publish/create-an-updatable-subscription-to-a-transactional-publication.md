---
title: "创建事务发布的可更新订阅 (Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "07/21/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "可更新事务性订阅"
  - "可更新事务订阅 SSMS"
ms.assetid: f9ef89ed-36f6-431b-8843-25d445ec137f
caps.latest.revision: 51
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 51
---
# 创建事务发布的可更新订阅 (Management Studio)

> [!NOTE]  
>  此功能在从 2012 到 2016 的 [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] 版本中仍然受支持。  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
 
配置可更新订阅上 **可更新订阅** 页 **新建订阅向导**。 只有为可更新订阅启用了事务发布，此页才可用。 有关启用可更新订阅的详细信息，请参阅 [对于事务发布启用更新订阅](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)。   
  
## 从发布服务器配置可更新订阅  

1. 连接到 Microsoft SQL Server Management Studio 中的发布服务器，然后展开服务器节点。

2. 展开 **“复制”** 文件夹，再展开 **“本地发布”** 文件夹。

3. 右键单击为更新订阅，请启用的事务发布，然后单击 **新订阅**。

4. 按照向导中的页，为订阅指定选项，如分发代理应在何处运行。

5. 在 **可更新订阅** 页 **新建订阅向导**, ，确保 **复制** 处于选中状态。

6. 选择从一个选项 **在发布服务器提交** 下拉列表︰

    * 若要使用立即更新订阅，请选择 **同时提交更改**。 如果选择此选项，并且发布允许排队更新订阅 （使用新建发布向导创建发布默认），则订阅属性 **update_mode** 设置为 **故障转移**。 此模式使您以后在必要时能够切换到排队更新。

    * 若要使用排队更新订阅，请选择 **更改进行排队并在可能时提交**。 如果选择此选项，该发布允许立即更新订阅 （使用新建发布向导创建发布默认） 和订阅服务器上正在运行 SQL Server 2005 或更高版本，则订阅属性 **update_mode** 设置为排队故障转移。 此模式使您以后在必要时能够切换到立即更新。

    有关切换更新模式的信息，请参阅 [模式之间切换更新为可更新事务性订阅](../../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md)。

7. **可更新订阅的登录名** 页将显示订阅使用立即更新或具有供 **update_mode** 设置为 **排队故障转移**。 在 **可更新订阅的登录名** 页上，指定对其进行即时更新订阅连接到发布服务器的链接的服务器。 连接用于在订阅服务器上激发的触发器，这些触发器用于将更改传播到发布服务器。 选择以下选项之一：

    * **创建链接的服务器使用 SQL Server 身份验证进行连接。** 如果尚未在订阅服务器和发布服务器之间定义远程服务器或链接服务器，则选择此选项。 复制会为您创建链接服务器。 所指定的帐户在发布服务器上必须已经存在。

    * **使用您指定的链接服务器或远程服务器。** 如果您定义了远程服务器或订阅服务器与发布服务器使用之间的链接的服务器，请选择此选项 [sp_addserver (TRANSACT-SQL)](../../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md), ，[sp_addlinkedserver (TRANSACT-SQL)](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md), ，SQL Server Management Studio 或另一种方法。

    有关链接的服务器帐户所需的权限的信息，请参阅 **排队更新订阅的** 的 [链接在此输入说明](../../../relational-databases/replication/security/secure-the-subscriber.md)。

8. 完成向导。

## 从订阅服务器配置可更新订阅


1. 连接到 SQL Server Management Studio，在订阅服务器，然后展开服务器节点。

2. 展开 **“复制”** 文件夹。

3. 用鼠标右键单击 **本地订阅** 文件夹，，然后单击 **新订阅**。

4. 在 **发布** 页 **新建订阅向导**, ，选择 **查找 SQL Server 发布服务器** 从 **Publisher** 下拉列表。

5. 在 **“连接到服务器”** 对话框中连接到发布服务器。

6. 选择用于在更新订阅启用的事务发布 **发布** 页。

7. 按照向导中的页，为订阅指定选项，如分发代理应在何处运行。

8. 在 **可更新订阅** 页上的新建订阅向导中，确保 **复制** 处于选中状态。

9. 选择从一个选项 **在发布服务器提交** 下拉列表︰

    * 若要使用立即更新订阅，请选择 **同时提交更改**。 如果选择此选项，并且发布允许排队更新订阅 （使用新建发布向导创建发布默认），则订阅属性 **update_mode** 设置为 **故障转移**。 此模式使您以后在必要时能够切换到排队更新。

    * 若要使用排队更新订阅，请选择 **更改进行排队并在可能时提交**。 如果选择此选项，该发布允许立即更新订阅 （使用新建发布向导创建发布默认） 和订阅服务器上正在运行 SQL Server 2005 或更高版本，则订阅属性 **update_mode** 将设置为排队 **故障转移**。 此模式使您以后在必要时能够切换到立即更新。

    有关切换更新模式的信息，请参阅 [模式之间切换更新为可更新事务性订阅](../../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md)。

10. **可更新订阅的登录名** 页将显示订阅使用立即更新或具有供 **update_mode** 将设置为排队 **故障转移**。 在 **可更新订阅的登录名** 页上，指定对其进行即时更新订阅连接到发布服务器的链接的服务器。 连接用于在订阅服务器上激发的触发器，这些触发器用于将更改传播到发布服务器。 选择以下选项之一：

    * **创建链接的服务器使用 SQL Server 身份验证进行连接。** 如果尚未在订阅服务器和发布服务器之间定义远程服务器或链接服务器，则选择此选项。 复制会为您创建链接服务器。 所指定的帐户在发布服务器上必须已经存在。

    * **使用您指定的链接服务器或远程服务器。** 如果您定义了远程服务器或订阅服务器与发布服务器使用之间的链接的服务器，请选择此选项 [sp_addserver (TRANSACT-SQL)](../../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md), ，[sp_addlinkedserver (TRANSACT-SQL)](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md), ，SQL Server Management Studio 或另一种方法。

    有关链接的服务器帐户所需的权限的信息，请参阅 **排队更新订阅的** 的 [链接在此输入说明](../../../relational-databases/replication/security/secure-the-subscriber.md)。

11. 完成向导。

## 另请参阅

[事务复制的可更新订阅](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)

[创建发布](../../../relational-databases/replication/publish/create-a-publication.md)

[使用 Transact-SQL 创建事务发布的可更新订阅](../../../relational-databases/replication/publish/create-updatable-subscription-to-transactional-publication.md) 
