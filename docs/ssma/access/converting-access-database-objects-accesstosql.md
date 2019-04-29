---
title: 转换访问数据库对象 (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases
- Access databases, converting schemas
- conversion
- conversion, converting schemas
- indexes, altering
- metadata
- metadata, altering
- metadata, converting
- migrating databases, one-click
- one-click migration
- schemas
- schemas, converting
- SQL
- SQL, converting
- syntax
- syntax, converting
- tables, altering
- translating Access to SQL Azure
- translating Access to SQL Server
ms.assetid: e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: c4bb3d1b6fdc57e1251e9c8ca39f0c7437ffb126
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63139013"
---
# <a name="converting-access-database-objects-accesstosql"></a>转换访问数据库对象 (AccessToSQL)
在访问数据库添加并连接到后[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure、 SSMA 显示访问元数据和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 数据库对象。 你可以现在选择访问数据库对象，然后将转换到架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 架构。  
  
## <a name="the-conversion-process"></a>转换过程  
将转换数据库对象采用访问元数据中的对象定义，将它们转换为等效[!INCLUDE[tsql](../../includes/tsql-md.md)]语法，并将此信息然后加载到项目。 然后，可以查看[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 对象和它们的属性使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 元数据资源管理器。  
  
> [!IMPORTANT]  
> 将对象转换不会创建中的对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 它仅将为对象定义，并将信息存储在 SSMA 项目中。  
  
在转换期间 SSMA 打印到输出窗格和错误、 警告和信息性消息错误列表窗格的状态。 使用此信息来确定是否需要修改您的 Access 数据库或转换过程来获取所需的转换结果。 此外可以使用中的信息[迁移准备 Access 数据库](preparing-access-databases-for-migration-accesstosql.md)主题，以确定什么将并不会进行转换。  
  
## <a name="setting-conversion-options"></a>设置转换选项  
在将对象转换之前, 查看中的项目转换选项**项目设置**对话框。 通过使用此对话框中，可以设置 SSMA 将索引的 memo 列、 主键、 外键约束、 时间戳和没有索引的表的转换。 有关详细信息，请参阅[项目设置 （转换）](https://msdn.microsoft.com/bcebc635-c638-4ddb-924c-b9ccfef86388)  
  
## <a name="conversion-results"></a>转换结果  
下表显示哪些访问对象会转换与生成的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 对象：  
  
|访问对象|生成的 SQL Server 对象|  
|-----------------|-------------------------------|  
|表|表|  
|column|column|  
|索引|索引|  
|外键 (foreign key)|外键 (foreign key)|  
|Query|view<br /><br />大多数 SELECT 查询转换为视图中。 其他查询，如更新查询不会迁移。<br /><br />采用参数的 SELECT 查询不会转换，也不会交叉表查询。|  
|报表|未转换|  
|窗体|未转换|  
|宏|未转换|  
|module|未转换|  
|默认值|默认值|  
|允许为零长度的列属性|检查约束|  
|列验证规则|检查约束|  
|表验证规则|检查约束|  
|主键 (primary key)|主键 (primary key)|  
  
## <a name="converting-access-objects"></a>转换访问对象  
若要将访问数据库对象，首先必须选择你想要将转换，然后让 SSMA 进行转换的对象。 若要在转换期间查看输出消息上**视图**菜单中，选择**输出**。  
  
**选择并将访问数据库对象转换为 SQL Server 或 SQL Azure 的语法**  
  
1.  在访问元数据资源管理器中，展开**访问元数据库**，然后展开**数据库**。  
  
2.  执行以下一项或多项操作：  
  
    -   若要将所有数据库，选择复选框旁边**数据库**。  
  
    -   若要将转换或省略单独的数据库，选择或清除的数据库名称旁边的复选框。  
  
    -   若要将转换或省略查询，再展开数据库，然后选中或清除**查询**复选框。  
  
    -   若要将转换或忽略各个表，展开数据库，展开**表**，然后选中或清除表旁边的复选框。  
  
3.  执行以下操作之一：  
  
    -   若要转换的架构，右键单击**数据库**，然后选择**转换架构**。  
  
        此外可以将单个对象的转换。 若要转换的对象，而不考虑该选择对象，右键单击该对象，并选择**转换架构**。  
  
        当已转换对象时，它将显示访问元数据资源管理器中以粗体显示。  
  
    -   若要将转换、 加载和迁移架构和数据在一个步骤中的，右键单击数据库，然后选择**转换、 加载和迁移**。  
  
4.  查看中的消息**输出**窗格和所有错误和警告中的**错误列表**窗格。  
  
## <a name="altering-tables-and-indexes"></a>更改表和索引  
转换到访问元数据后[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 元数据，并加载到对象之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，可以更改[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 表和索引。  
  
**若要更改表或索引属性**  
  
1.  在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 元数据资源管理器中，选择你想要更改的索引的表。  
  
2.  上**表**选项卡上，单击你想要更改然后输入或选择新设置的属性。 例如，可以将 nvarchar(15) 更改为 nvarchar(20)，也可以选择一个复选框以使表格列可以为 null。  
  
    将光标移出已更改的属性的单元格。 可以通过单击其他行或按 Tab 键来执行此操作。  
  
3.  单击 **“应用”**。  
  
现在可以在查看代码中的更改**SQL**选项卡。  
  
## <a name="next-step"></a>下一步  
迁移过程中的下一步是[转换后的数据库对象加载到 SQL Server](loading-converted-database-objects-into-sql-server-accesstosql.md)  
  
## <a name="see-also"></a>请参阅  
[Access 数据库迁移到 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
