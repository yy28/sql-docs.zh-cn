---
title: "设置订阅的过期期限 | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "订阅 [SQL Server 复制], 过期"
  - "过期 [SQL Server 复制]"
  - "保持期 [SQL Server 复制]"
  - "停用订阅"
ms.assetid: 542f0613-5817-42d0-b841-fb2c94010665
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# 设置订阅的过期期限
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中设置订阅的过期期限。 订阅的过期期限决定了订阅在经过多长时间后过期并被删除。 有关详细信息，请参阅 [Subscription Expiration and Deactivation](../../../relational-databases/replication/subscription-expiration-and-deactivation.md)。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [建议](#Recommendations)  
  
-   **设置订阅的过期期限，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Recommendations"></a> 建议  
  
-   订阅过期期限也称为“发布保持期” 。 合并复制元数据的清除依赖于此设置：  
  
    -   在到达保持期之前，复制无法清除发布数据库和订阅数据库中的元数据。 在为保持期指定较大值时务必谨慎，因为这可能对复制性能产生负面影响。 如果能很有把握地预测出所有订阅服务器都将在该时间段内定期同步，则建议使用较低的设置。  
  
         合并发布的保持期具有 24 小时的宽限期，以适应处于不同时区中的订阅服务器。 例如，如果将保持期设置为 1 天，则实际的保持期为 48 小时。  
  
    -   可以指定订阅永不过期，但是强烈建议您不要使用此值，因为这样将无法清除元数据。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 设置订阅的过期期限 **常规** 页 **发布属性-\< 发布>** 对话框。 有关访问此对话框的详细信息，请参阅 [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
#### 设置订阅的过期期限  
  
1.  在 **订阅过期** 部分 **常规** 页 **发布属性-\< 发布>** 对话框框中，指定订阅是否应该过期。  
  
2.  如果它们应该过期，请指定一个过期时间段。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用复制存储过程在创建发布时设置此值或以后修改此值。  
  
#### 为快照或事务发布设置订阅过期时间  
  
1.  在发布服务器上，执行 [sp_addpublication](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)。 以小时为单位为 **@retention**指定所需的订阅过期时间。 默认的过期时间为 336 个小时。 有关详细信息，请参阅 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)。  
  
#### 为合并发布设置订阅过期时间  
  
1.  在发布服务器上，执行 [sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)。 为 **@retention**指定所需的订阅过期时间值。 指定的过期期限为用于表示的单位 **@retention_period_unit**, ，可以是以下项之一︰  
  
    -   **1** = 周  
  
    -   **2** = 月  
  
    -   **3** = 年  
  
     默认的过期时间为 14 天。 有关详细信息，请参阅 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)。  
  
#### 更改快照或事务发布的订阅过期时间  
  
1.  在发布服务器上，执行 [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)。 为 **@property** 指定 **retention** ，并以小时为单位为 **@value**指定新的订阅过期时间。  
  
#### 更改合并发布的订阅过期时间  
  
1.  在发布服务器上，执行 [sp_helpmergepublication](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md), ，并指定 **@publication** 和 **@publisher**。 记下的值 **retention_period_unit** 在结果集中，可以是以下之一︰  
  
    -   **0** = 某一天  
  
    -   **1** = 周  
  
    -   **2** = 月  
  
    -   **3** = 年  
  
2.  在发布服务器上，执行 [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)。 为 **@property** 指定 **retention** ，并以步骤 1 中的保持期单位为 **@value**指定新的订阅过期时间。  
  
3.  （可选）在发布服务器上，执行 [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)。 指定 **retention_period_unit** 为 **@property** 和新的订阅过期期限单位 **@value**。  
  
## 另请参阅  
 [复制系统存储过程概念](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [订阅过期和停用](../../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  