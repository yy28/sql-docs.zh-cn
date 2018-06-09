---
title: 链接到 SQL Server 的 Azure SQL 数据库的访问应用程序 |Microsoft 文档
ms.prod: sql
ms.custom: ''
ms.date: 08/17/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
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
caps.latest.revision: 19
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: e64bd412bc26dd2ac3cae24211591caa11f12031
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2018
ms.locfileid: "34774063"
---
# <a name="linking-access-applications-to-sql-server---azure-sql-db-accesstosql"></a>链接到 SQL Server 的 Azure SQL DB (AccessToSQL) 访问应用程序
如果你想要使用现有的 Access 应用程序，用于[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，你可以将原始 Access 表链接到已迁移[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 表。 链接会修改你的 Access 数据库，以便你的查询、 窗体、 报表和数据访问页使用中的数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 数据库而不是你的 Access 数据库中的数据。  
  
> [!NOTE]  
> 访问表保持在 Access 中，但不是更新连同[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 更新。 链接表，并验证功能后，你可能想要删除访问表。  
  
## <a name="linking-access-and-sql-server-tables"></a>链接的访问权限和 SQL Server 表  
当您链接到一个 Access 表[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 表，Jet 数据库引擎用来存储连接信息和表元数据，但数据存储在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 此链接允许尽管实际的表和数据都是在访问应用程序访问表运行[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。  
  
> [!NOTE]  
> 如果你使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]链接访问表上以明文形式存储身份验证，你的密码。 我们建议使用 Windows 身份验证。  
  
**若要链接表**  
  
1.  在访问元数据资源管理器，选择你想要链接的表。  
  
2.  右键单击**表**，然后选择**链接**。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant (SSMA) 用于访问备份的原始访问表，并创建链接的表。  
  
链接表后，SSMA 中的表显示时带有小链接图标。 在 Access 中，表会显示与"链接"图标，它是带箭头指向全球。  
  
当你在 Access 中打开表时，使用键集游标检索的数据。 因此，对于大型表，不一次检索所有数据。 但是，表中浏览时，访问将检索根据需要的其他数据。  
  
> [!IMPORTANT]  
> 若要使用 Azure 数据库的 access 表链接，你需要 SQL Server 本机 Client(SNAC) 版本 10.5 或更高版本。   
> 你可以获取最新版本从 SNAC [Microsoft® SQL Server® 2008 R2 功能包](http://go.microsoft.com/fwlink/?LinkId=196940)。  
  
## <a name="unlinking-access-tables"></a>取消链接访问表  
当您取消链接从一个 Access 表[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 表，SSMA 还原原始访问表及其数据。  
  
**若要取消链接表**  
  
1.  在访问元数据资源管理器，选择你想要取消链接的表。  
  
2.  右键单击**表**，然后选择**取消链接**。  
  
## <a name="linking-tables-to-a-different-server"></a>将表链接到其他服务器  
如果已访问表链接到一个 SQL Server 实例，并且你以后要更改链接到另一个实例，则必须重新链接表。  
  
**若要链接到其他服务器表**  
  
1.  在访问元数据资源管理器，选择你想要取消链接的表。  
  
2.  右键单击**表**，然后选择**取消链接**。  
  
3.  单击**重新连接到 SQL Server**按钮。  
  
4.  连接到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或你想要 Access 表链接的 SQL Azure。  
  
5.  在访问元数据资源管理器，选择你想要链接的表。  
  
6.  右键单击**表**，然后选择**链接**。  
  
## <a name="updating-linked-tables"></a>更新链接的表  
如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 表定义会被更改，你可以取消链接，然后使用本主题前面所演示的过程重新链接 SSMA 中的表。 您还可以通过使用访问更新表。  
  
**通过使用访问更新链接的表**  
  
1.  打开访问数据库。  
  
2.  在**对象**列表中，单击**表**。  
  
3.  右键单击链接的表，然后选择**链接表管理器**。  
  
4.  选择你想要更新，，然后单击每个链接表旁边的复选框**确定**。  
  
## <a name="possible-post-migration-issues"></a>可能存在的迁移后问题  
以下各节后将数据库迁移到的访问从可能发生的现有访问应用程序的列表问题[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，然后将链接表，以及原因和解决方法。  
  
### <a name="slow-performance-with-linked-tables"></a>使用链接表的慢速性能  
**原因：** 某些查询后，可能会慢扩大原因如下：  
  
-   应用程序依赖于中不存在的函数[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，这会导致 Jet 以下载可本地表运行 SELECT 查询。  
  
-   更新或删除很多行的查询将通过 Jet 中作为参数化查询发送的每一行。  
  
**解决方法：** 将运行速度缓慢的查询转换为传递查询、 存储的过程或视图。 将转换为传递查询具有以下问题：  
  
-   传递查询不能修改。 修改查询结果，或添加新记录，必须完成的另一个方法，例如通过让显式**修改**或**添加**已绑定到查询你窗体上的按钮。  
  
-   某些查询需要用户输入，但传递的查询不支持用户输入。 通过 Visual Basic for Applications (VBA) 代码提示输入参数，或用作输入控件的窗体，可以获取用户输入。 在这两种情况下，VBA 代码将提交到服务器的用户输入的查询。  
  
### <a name="auto-increment-columns-are-not-updated-until-the-record-is-updated"></a>更新的记录之前，不会更新自动递增列  
**原因：** 后调用中 Jet RecordSet.AddNew，自动递增列就可更新的记录之前。 不能在同时运行[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 仅在保存新的记录之后，标识列的新值的新值才可用。  
  
**解决方法：** 访问标识字段之前，运行下面的 Visual Basic for Applications (VBA) 代码：  
  
```  
Recordset.Update  
Recordset.Move 0,  
Recordset.LastModified  
```  
  
### <a name="new-records-are-not-available"></a>新记录将不可用  
**原因：** 添加到记录时[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或通过使用 VBA，如果表的唯一索引字段具有默认值，并且你没有将值赋给该字段未显示新记录之前重新打开中的表的 SQL Azure 表[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 如果你尝试从新的记录中获取一个值，你将收到以下错误消息：  
  
`Run-time error '3167' Record is deleted.`  
  
**解决方法：** 当打开[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 表使用的 VBA 代码，包括`dbSeeChanges`选项，如下面的示例所示：  
  
`Set rs = db.OpenRecordset("TestTable", dbOpenDynaset, dbSeeChanges)`  
  
### <a name="after-migration-some-queries-will-not-allow-the-user-to-add-a-new-record"></a>迁移后，某些查询将不允许用户添加一条新记录  
**原因：** 如果查询不包含唯一索引中包含的所有列，则无法使用查询中添加新值。  
  
**解决方法：** 确保至少一个唯一索引中包含的所有列都是查询的一部分。  
  
### <a name="you-cannot-modify-a-linked-table-schema-with-access"></a>无法修改具有访问权限的链接的表架构  
**原因：** 之后迁移数据和链接表，用户无法修改中访问的表的架构。  
  
**解决方法：** 使用修改表架构[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]，然后更新中访问的链接。  
  
### <a name="hyperlink-functionality-is-lost-after-migrating-data"></a>超链接的功能在迁移后将丢失数据  
**原因：** 在迁移后数据，列中的超链接失去其功能，并且变得非常简单**nvarchar (max)** 列。  
  
**解决方法：** None。  
  
### <a name="some-sql-server-data-types-are-not-supported-by-access"></a>某些 SQL Server 数据类型不受访问  
**原因：** 如果更高版本更新你[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 表，以包含访问权限，不支持的数据类型不能在 Access 中打开该表。  
  
**解决方法：** ，可以定义仅返回这些行支持的数据类型与访问查询。  
  
## <a name="see-also"></a>另请参阅  
[将访问数据库迁移到 SQL Server](http://msdn.microsoft.com/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
