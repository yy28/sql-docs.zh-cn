---
title: 链接到 SQL Server-Azure SQL 数据库的访问应用程序 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/17/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases, linking to SQL Azure
- Access databases, linking to SQL Server
- auto-increment columns
- data types, unsupported
- hyperlink columns
- linking tables
- migrating databases, post-migration issues
- post-migration issues
- reference, post-migration issues
- refreshing linked tables
- slow performance
- unlinking tables
ms.assetid: 82374ad2-7737-4164-a489-13261ba393d4
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: 20efdf681baa8305b3b2be08b2e9f3efe999d3fa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62760137"
---
# <a name="linking-access-applications-to-sql-server---azure-sql-db-accesstosql"></a>链接到 SQL Server-Azure SQL DB (AccessToSQL) 访问应用程序
如果想要使用现有的 Access 应用程序，用于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，你可以将原始 Access 表链接到已迁移[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 表。 链接会修改你的 Access 数据库，以便你的查询、 窗体、 报表和数据访问页使用中的数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 数据库而不是你的 Access 数据库中的数据。  
  
> [!NOTE]  
> 访问表保留在 Access 中，但不是会一起使用更新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 更新。 在链接表，并验证功能后，你可能想要删除访问表。  
  
## <a name="linking-access-and-sql-server-tables"></a>链接 Access 和 SQL Server 表  
当链接到的访问权限表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 表，Jet 数据库引擎用来存储连接信息和表的元数据，但数据存储在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 此链接允许访问应用程序即使在实际表和数据是针对访问表运行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。  
  
> [!NOTE]  
> 如果使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中链接的 Access 表上以明文形式存储身份验证，你的密码。 我们建议使用 Windows 身份验证。  
  
**若要链接表**  
  
1.  在访问元数据资源管理器，选择想要链接的表。  
  
2.  右键单击**表**，然后选择**链接**。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 迁移助手 (SSMA) for Access 备份原始 Access 表并创建链接的表。  
  
链接表之后，在 SSMA 中的表显示时带有小链接图标。 在 Access 中，表显示"链接"图标，它是全球且指向它的箭头。  
  
当在 Access 中打开表时，请使用由键集游标检索的数据。 因此，对于大型表，所有数据不会检索一次。 但是，在表中浏览时，Access 会检索必要的其他数据。  
  
> [!IMPORTANT]  
> 若要使用的 Azure 数据库的 access 表链接，你需要 SQL Server 本机 Client(SNAC) 版本 10.5 或更高版本。   
> 你可以获取最新版本从 SNAC [Microsoft® SQL Server® 2008 R2 功能包](https://go.microsoft.com/fwlink/?LinkId=196940)。  
  
## <a name="unlinking-access-tables"></a>取消链接访问表  
取消链接从一个访问表时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 表，SSMA 还原原始访问表及其数据。  
  
**若要取消链接表**  
  
1.  在访问元数据资源管理器，选择你想要取消链接的表。  
  
2.  右键单击**表**，然后选择**取消链接**。  
  
## <a name="linking-tables-to-a-different-server"></a>将表链接到另一台服务器  
如果 Access 表链接到一个 SQL Server 实例，并且你稍后想要更改链接到另一个实例，则必须重新链接表。  
  
**若要将表链接到其他服务器**  
  
1.  在访问元数据资源管理器，选择你想要取消链接的表。  
  
2.  右键单击**表**，然后选择**取消链接**。  
  
3.  单击**重新连接到 SQL Server**按钮。  
  
4.  连接到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或你想要 Access 表链接的 SQL Azure。  
  
5.  在访问元数据资源管理器，选择想要链接的表。  
  
6.  右键单击**表**，然后选择**链接**。  
  
## <a name="updating-linked-tables"></a>更新链接的表  
如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 表定义会被更改，您可以取消链接，然后使用本主题中前面所示的过程重新链接在 SSMA 中的表。 此外可以使用访问权限来更新表。  
  
**若要通过使用访问更新链接的表**  
  
1.  打开 Access 数据库。  
  
2.  在中**对象**列表中，单击**表**。  
  
3.  右键单击一个链接的表，然后依次**链接表管理器**。  
  
4.  选择你想要更新，然后单击每个链接表旁边的复选框**确定**。  
  
## <a name="possible-post-migration-issues"></a>可能的迁移后问题  
下面的部分将从访问到迁移数据库之后在现有访问应用程序中可能出现的列表问题[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，然后将链接表以及原因和解决方法。  
  
### <a name="slow-performance-with-linked-tables"></a>使用链接表的慢速性能  
**原因：** 某些查询后，可能会慢扩大原因如下：  
  
-   应用程序依赖于中不存在的函数[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，这会导致 Jet 提取本地表运行 SELECT 查询。  
  
-   更新或删除多行的查询的每一行发送 Jet 通过作为参数化查询。  
  
**解决方法：** 将运行速度缓慢的查询转换为传递查询、 存储的过程或视图。 将转换为传递查询具有以下问题：  
  
-   不能修改传递查询。 修改查询结果或添加新记录中必须进行的另一个方法，如通过采用显式**修改**或**添加**已绑定到查询在窗体上的按钮。  
  
-   某些查询需要用户输入，但传递的查询不支持用户输入。 通过 Visual Basic for Applications (VBA) 代码提示输入参数，或用作输入的控件的窗体，可以获取用户输入。 在这两种情况下，VBA 代码提交到服务器的用户输入查询。  
  
### <a name="auto-increment-columns-are-not-updated-until-the-record-is-updated"></a>对记录进行更新之前，不会更新自动递增列  
**原因：** 在调用之后 RecordSet.AddNew Jet 中，自动递增列是可用之前更新该记录。 不能同时在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 保存新记录后，只是可用的标识列的新值的新值。  
  
**解决方法：** 访问标识字段之前运行以下 Visual Basic for Applications (VBA) 代码：  
  
```  
Recordset.Update  
Recordset.Move 0,  
Recordset.LastModified  
```  
  
### <a name="new-records-are-not-available"></a>新记录不可用  
**原因：** 添加一条记录时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或通过使用 VBA 中，如果表的唯一索引字段具有默认值，并且您没有将值赋给该字段中，新记录不会出现直到您重新打开的表中的 SQL Azure 表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 如果尝试从新的记录中获取一个值，你将收到以下错误消息：  
  
`Run-time error '3167' Record is deleted.`  
  
**解决方法：** 当打开[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 表使用 VBA 代码中，包括`dbSeeChanges`选项，如以下示例所示：  
  
`Set rs = db.OpenRecordset("TestTable", dbOpenDynaset, dbSeeChanges)`  
  
### <a name="after-migration-some-queries-will-not-allow-the-user-to-add-a-new-record"></a>迁移后，某些查询将不允许用户将添加一条新记录  
**原因：** 如果查询不包含在唯一索引中包含的所有列，不能使用查询中添加新值。  
  
**解决方法：** 确保至少一个唯一索引中包含的所有列的查询的一部分。  
  
### <a name="you-cannot-modify-a-linked-table-schema-with-access"></a>无法修改具有访问权限的链接的表架构  
**原因：** 迁移数据和链接表后, 用户无法修改中访问表的架构。  
  
**解决方法：** 通过使用来修改表架构[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，然后更新中访问的链接。  
  
### <a name="hyperlink-functionality-is-lost-after-migrating-data"></a>迁移后将超链接的功能会丢失数据  
**原因：** 在迁移后数据列中的超链接会丢失其功能和变得非常简单**nvarchar （max)** 列。  
  
**解决方法：** 无。  
  
### <a name="some-sql-server-data-types-are-not-supported-by-access"></a>某些 SQL Server 数据类型不受访问  
**原因：** 如果更高版本更新你[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 表来包含访问权限，不支持的数据类型不能在 Access 中打开表。  
  
**解决方法：** 可以定义只返回这些行与支持的数据类型的访问查询。  
  
## <a name="see-also"></a>另请参阅  
[Access 数据库迁移到 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
