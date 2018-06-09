---
title: 转换访问数据库对象 (AccessToSQL) |Microsoft 文档
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
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
caps.latest.revision: 22
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 36d73e04296346bd0c44a8459ec157d437df8583
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2018
ms.locfileid: "34773473"
---
# <a name="converting-access-database-objects-accesstosql"></a>转换访问数据库对象 (AccessToSQL)
在已添加访问数据库并连接到后[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure、 SSMA 用于访问显示元数据和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 数据库对象。 你可以现在选择访问数据库对象，然后将转换到的架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 架构。  
  
## <a name="the-conversion-process"></a>转换过程  
转换数据库对象获取访问元数据中的对象定义，并将它们转换为等效[!INCLUDE[tsql](../../includes/tsql_md.md)]语法，然后将此信息加载到项目。 然后，您可以查看[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 对象和通过使用其属性[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 元数据资源管理器。  
  
> [!IMPORTANT]  
> 转换对象不会创建中的对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 它仅将转换的对象定义，并将信息存储在 SSMA 项目。  
  
在转换期间，SSMA 输出到输出窗格中，和错误、 警告和到错误列表窗格中的信息性消息的状态。 使用此信息来确定是否需要修改你的 Access 数据库或您的转换过程，以获取所需的转换结果。 你还可以使用中的信息[准备迁移的 Access 数据库](http://msdn.microsoft.com/en-us/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)主题，以确定将和将不会转换。  
  
## <a name="setting-conversion-options"></a>设置转换选项  
在将对象转换之前, 查看中的项目转换选项**项目设置**对话框。 通过使用此对话框中，你可以设置 SSMA 将索引的 memo 列、 主键、 外键约束、 时间戳和没有索引的表的转换。 有关详细信息，请参阅[项目设置 （转换）](http://msdn.microsoft.com/en-us/bcebc635-c638-4ddb-924c-b9ccfef86388)  
  
## <a name="conversion-results"></a>转换结果  
下表显示访问对象都转换，以及产生[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 对象：  
  
|访问对象|生成的 SQL Server 对象|  
|-----------------|-------------------------------|  
|表|表|  
|column|column|  
|索引|索引|  
|外键 (foreign key)|外键 (foreign key)|  
|Query|view<br /><br />最 SELECT 查询将转换为视图中。 其他查询，如更新查询，不会迁移。<br /><br />采用参数的 SELECT 查询不会转换，也不会交叉表查询。|  
|报表|不转换|  
|窗体|不转换|  
|宏|不转换|  
|module|不转换|  
|默认值|默认值|  
|允许零长度列属性|检查约束|  
|列验证规则|检查约束|  
|表验证规则|检查约束|  
|主键 (primary key)|主键 (primary key)|  
  
## <a name="converting-access-objects"></a>转换访问对象  
若要访问数据库对象的转换，首先必须选择你想要转换，则具有 SSMA 进行转换的对象。 若要查看输出消息在转换期间上,**视图**菜单上，选择**输出**。  
  
**选择并将访问数据库对象转换为 SQL Server 或 SQL Azure 语法**  
  
1.  在访问元数据资源管理器中，展开**访问元数据库**，然后展开**数据库**。  
  
2.  执行以下一项或多项操作：  
  
    -   若要转换的所有数据库，请旁边选中的复选框**数据库**。  
  
    -   若要将转换或省略单个数据库，选择或清除数据库名称旁边的复选框。  
  
    -   若要将转换或省略查询，展开数据库，然后选中或清除**查询**复选框。  
  
    -   若要将转换或省略各个表，展开数据库，展开**表**，然后选择或清除的表旁边的复选框。  
  
3.  执行以下操作之一：  
  
    -   若要转换的架构，右键单击**数据库**和选择**转换架构**。  
  
        你还可以将单个对象的转换。 要转换的对象，而所选对象，右键单击对象，然后选择**转换架构**。  
  
        转换后的对象，它会在访问元数据资源管理器以粗体显示。  
  
    -   若要将转换、 加载和迁移架构和数据在一个步骤中的，右键单击数据库并选择**转换、 加载和迁移**。  
  
4.  查看中的消息**输出**窗格以及任何错误和警告中的**错误列表**窗格。  
  
## <a name="altering-tables-and-indexes"></a>更改表和索引  
在转换到的访问元数据后[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 元数据，并在加载到对象之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，你可以更改[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 表和索引。  
  
**若要更改表或索引的属性**  
  
1.  在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 元数据资源管理器，选择你想要更改的索引的表。  
  
2.  上**表**选项卡上，单击你想要更改然后输入或选择新的设置的属性。 例如，可以更改 nvarchar(15) 到 nvarchar(20)，也可以选择复选框以将表列可以为 null。  
  
    将光标移出已更改的属性单元格。 可以通过单击另一行或按 Tab 键来执行此操作。  
  
3.  单击 **“应用”**。  
  
你现在可以查看代码中的更改上**SQL**选项卡。  
  
## <a name="next-step"></a>下一步  
迁移过程的下一步是[加载到 SQL Server 的已转换的数据库对象](http://msdn.microsoft.com/en-us/4e854eee-b10c-4f0b-9d9e-d92416e6f2ba)  
  
## <a name="see-also"></a>请参阅  
[将访问数据库迁移到 SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
