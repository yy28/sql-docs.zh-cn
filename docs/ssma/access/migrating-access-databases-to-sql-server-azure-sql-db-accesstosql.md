---
title: 将 Access 数据库迁移到 SQL Server-Azure SQL 数据库 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/15/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- instructions, migration
- migrating databases, overview
- overview, migration process
- procedure, migration
- recommended migration process
ms.assetid: 76a3abcf-2998-4712-9490-fe8d872c89ca
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: b15ecd732acf373dbc5cee817983305c1d792fe4
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "63453587"
---
# <a name="migrating-access-databases-to-sql-server---azure-sql-db-accesstosql"></a>Access 数据库迁移到 SQL Server-Azure SQL DB (AccessToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) 是一个工具，提供了一个全面的环境，可帮助你快速访问将数据库迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 可以通过使用 SSMA，评审访问权限和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 数据库对象、 评估迁移的 Access 数据库、 访问数据库对象转换、 加载到它们[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，然后将数据迁移。  
  
## <a name="recommended-migration-process"></a>建议的迁移过程  
为了成功将对象和数据迁移从 Access 到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，使用以下过程：  
  
1.  [创建新的 SSMA 项目](creating-and-managing-projects-accesstosql.md)。 创建项目之后，你可以[设置项目选项](setting-conversion-and-migration-options-accesstosql.md)，包括转换选项、 迁移选项和数据类型映射。  
  
2.  [添加 Access 数据库文件](adding-and-removing-access-database-files-accesstosql.md)到项目。  
  
    您可以添加单独的文件，包括网络的计算机上找到的文件。  
  
3.  [连接到 SQL Server 的目标实例](connecting-to-sql-server-accesstosql.md)或[连接到 SQL Azure 的目标实例](connecting-to-azure-sql-db-accesstosql.md)。  
  
    你可以连接到 SQL Server 或 SQL Azure。  
  
4.  若要自定义一个或多个访问数据库之间的映射并[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 架构[映射源和目标数据库](mapping-source-and-target-databases-accesstosql.md)。  
  
5.  （可选） 可以[创建评估报告](assessing-access-database-objects-for-conversion-accesstosql.md)来确定访问数据库对象是否可以成功转换为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。  
  
6.  [转换访问数据库对象](converting-access-database-objects-accesstosql.md)到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 对象定义。  
  
7.  [转换后的数据库对象加载到 SQL Server](loading-converted-database-objects-into-sql-server-accesstosql.md)。  
  
    您可以加载到的数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 使用 SSMA，也可以保存[!INCLUDE[tsql](../../includes/tsql-md.md)]脚本。  
  
8.  [将访问的数据迁移到 SQL Server](migrating-access-data-into-sql-server-azure-sql-db-accesstosql.md)。  
  
    > [!NOTE]  
    > 可以将转换、 加载和迁移架构和一个步骤中的数据。 若要执行一次单击迁移，请单击**转换、 加载和迁移**按钮。  
  
9. 如果想要使用中的数据将 Access 应用程序[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，使用[Access 表链接到 SQL Server 表](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)。  
  
此外可以使用迁移向导可引导您完成此过程。 有关详细信息，请参阅[迁移向导](migration-wizard-accesstosql.md)。  
  
## <a name="see-also"></a>另请参阅  
[开始使用用于访问 SQL Server 迁移助手](getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)  
[为迁移准备 Access 数据库](preparing-access-databases-for-migration-accesstosql.md)
