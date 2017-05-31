---
title: "创建事务发布的可更新订阅 | Microsoft Docs"
ms.custom: 
ms.date: 07/21/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- updatable transactional subscriptions
- updateable transactional subscriptions, SSMS
ms.assetid: f9ef89ed-36f6-431b-8843-25d445ec137f
caps.latest.revision: 51
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 94a6afee0fbc828b7c3036cfc4d1282b71674384
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="create-an-updatable-subscription-to-a-transactional-publication"></a>创建事务发布的可更新订阅

> [!NOTE]  
>  此功能在从 2012 到 2016 的 [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] 版本中仍然受支持。  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
 
可以在“新建订阅向导”的“可更新订阅”页上配置可更新订阅。**** 只有为可更新订阅启用了事务发布，此页才可用。 有关启用可更新订阅的详细信息，请参阅[为事务发布启用更新订阅](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)。   
  
## <a name="to-configure-an-updatable-subscription-from-the-publisher"></a>从发布服务器配置可更新订阅  

1. 在 Microsoft SQL Server Management Studio 中连接到发布服务器，然后展开服务器节点。

2. 展开 **“复制”** 文件夹，再展开 **“本地发布”** 文件夹。

3. 右键单击为更新订阅启用的事务发布，然后单击“新建订阅”。****

4. 按照向导中的页，为订阅指定选项，如分发代理应在何处运行。

5. 在“新建订阅向导”的“可更新订阅”页上，确保已选中“复制”。****

6. 从“在发布服务器提交”下拉列表中选择一个选项：****

    * 若要使用立即更新订阅，请选择“同时提交更改”。**** 如果选择此选项，并且发布允许排队更新订阅（使用新建发布向导所创建发布的默认设置），则订阅属性 **update_mode** 将设置为“故障转移”。**** 此模式使您以后在必要时能够切换到排队更新。

    * 若要使用排队更新订阅，请选择“对更改进行排队并在可能时提交”。**** 如果选择此选项且发布允许立即更新订阅（使用新建发布向导所创建发布的默认设置），而且订阅服务器运行的是 SQL Server 2005 或更高版本，则订阅属性 **update_mode** 将设置为排队故障转移。 此模式使您以后在必要时能够切换到立即更新。

    有关切换更新模式的详细信息，请参阅[切换可更新事务性订阅的更新模式](../../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md)。

7. 对于使用立即更新或将 **update_mode** 设置为**排队故障转移**的订阅，显示“用于可更新订阅的登录名”页。**** 在“用于可更新订阅的登录名”页上，指定链接服务器，通过此服务器可与发布服务器建立连接，以便立即更新订阅。**** 连接用于在订阅服务器上激发的触发器，这些触发器用于将更改传播到发布服务器。 选择以下选项之一：

    * **创建使用 SQL Server 身份验证进行连接的链接服务器。** 如果尚未在订阅服务器和发布服务器之间定义远程服务器或链接服务器，则选择此选项。 复制会为您创建链接服务器。 所指定的帐户在发布服务器上必须已经存在。

    * **使用您指定的链接服务器或远程服务器。** 如果已使用 [sp_addserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)、[sp_addlinkedserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)、SQL Server Management Studio 或其他方法在订阅服务器和发布服务器之间定义了远程服务器或链接服务器，请选择此选项。

    有关链接服务器帐户所需权限的信息，请参阅[在此处输入链接说明](../../../relational-databases/replication/security/secure-the-subscriber.md)的**排队更新订阅**部分。

8. 完成向导。

## <a name="to-configure-an-updatable-subscription-from-the-subscriber"></a>从订阅服务器配置可更新订阅


1. 在 SQL Server Management Studio 中连接到订阅服务器，然后展开服务器节点。

2. 展开 **“复制”** 文件夹。

3. 右键单击 **“本地订阅”** 文件夹，再单击 **“新建订阅”**。

4. 在“新建订阅向导”的“发布”页上，从“发布服务器”下拉列表中选择“查找 SQL Server 发布服务器”。****

5. 在 **“连接到服务器”** 对话框中连接到发布服务器。

6. 在“发布”页上，选择为更新订阅启用的事务发布。****

7. 按照向导中的页，为订阅指定选项，如分发代理应在何处运行。

8. 在“新建订阅向导”的“可更新订阅”页上，确保已选中“复制”。****

9. 从“在发布服务器提交”下拉列表中选择一个选项：****

    * 若要使用立即更新订阅，请选择“同时提交更改”。**** 如果选择此选项，并且发布允许排队更新订阅（使用新建发布向导所创建发布的默认设置），则订阅属性 **update_mode** 将设置为“故障转移”。**** 此模式使您以后在必要时能够切换到排队更新。

    * 若要使用排队更新订阅，请选择“对更改进行排队并在可能时提交”。**** 如果选择此选项且发布允许立即更新订阅（使用新建发布向导所创建发布的默认设置），而且订阅服务器运行的是 SQL Server 2005 或更高版本，则订阅属性 **update_mode** 将设置为排队**故障转移**。 此模式使您以后在必要时能够切换到立即更新。

    有关切换更新模式的详细信息，请参阅[切换可更新事务性订阅的更新模式](../../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md)。

10. 对于使用立即更新或将 **update_mode** 设置为排队**故障转移**的订阅，显示“用于可更新订阅的登录名”页。**** 在“用于可更新订阅的登录名”页上，指定链接服务器，通过此服务器可与发布服务器建立连接，以便立即更新订阅。**** 连接用于在订阅服务器上激发的触发器，这些触发器用于将更改传播到发布服务器。 选择以下选项之一：

    * **创建使用 SQL Server 身份验证进行连接的链接服务器。** 如果尚未在订阅服务器和发布服务器之间定义远程服务器或链接服务器，则选择此选项。 复制会为您创建链接服务器。 所指定的帐户在发布服务器上必须已经存在。

    * **使用您指定的链接服务器或远程服务器。** 如果已使用 [sp_addserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)、[sp_addlinkedserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)、SQL Server Management Studio 或其他方法在订阅服务器和发布服务器之间定义了远程服务器或链接服务器，请选择此选项。

    有关链接服务器帐户所需权限的信息，请参阅[在此处输入链接说明](../../../relational-databases/replication/security/secure-the-subscriber.md)的**排队更新订阅**部分。

11. 完成向导。

## <a name="see-also"></a>另请参阅

[Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)

[Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)

[使用 Transact-SQL 创建事务发布的可更新订阅](../../../relational-databases/replication/publish/create-updatable-subscription-to-transactional-publication.md) 


