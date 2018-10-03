---
title: 迁移的 Oracle 数据库移到 SQL Server (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 04/22/2018
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1d196dd6-4322-4c98-bb72-602c57d96134
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 9e746d1df201349011d24fc0de007c74ba0073b0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47651185"
---
# <a name="migrating-oracle-databases-to-sql-server-oracletosql"></a>将 Oracle 数据库迁移到 SQL Server (OracleToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 迁移助手 (SSMA) for Oracle 是一个全面的环境，可帮助你快速迁移到的 Oracle 数据库[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，Azure SQL DB 或 Azure SQL 数据仓库。 通过使用 SSMA for Oracle，可以查看数据库对象和数据、 评估要迁移的数据库，迁移到的数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，Azure SQL DB 或 Azure SQL 数据仓库，然后将数据迁移到和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，Azure SQL DB 或 Azure SQL 数据仓库。 请注意，不能将 SYS 和系统 Oracle 架构迁移。
  
## <a name="recommended-migration-process"></a>建议的迁移过程  
为了成功将对象和数据迁移到的 Oracle 数据库从[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，Azure SQL DB 或 Azure SQL 数据仓库中，使用以下过程：
  
1.  [创建新的 SSMA 项目](working-with-ssma-projects-oracletosql.md)。  
  
    创建项目后，可以设置项目转换、 迁移和类型映射选项。 有关项目设置的信息，请参阅[设置项目选项&#40;OracleToSQL&#41;](../../ssma/oracle/setting-project-options-oracletosql.md)。 有关如何自定义数据类型映射的信息，请参阅[映射 Oracle 和 SQL Server 数据类型&#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md)。  
  
2.  [连接到 Oracle 数据库服务器](connecting-to-oracle-database-oracletosql.md)。  
  
3.  [连接到 SQL server 实例](connecting-to-sql-server-oracletosql.md)。  
  
4.  [将 Oracle 数据库架构映射到 SQL Server 数据库架构](mapping-oracle-schemas-to-sql-server-schemas-oracletosql.md)。  
  
5.  （可选）[创建评估报告](assessing-oracle-schemas-for-conversion-oracletosql.md)来评估用于转换数据库对象和估计的转换时间。  
  
6.  [Oracle 数据库架构转换为 SQL Server 架构](converting-oracle-schemas-oracletosql.md)。  
  
7.  [转换后的数据库对象加载到 SQL Server](loading-converted-database-objects-into-sql-server-oracletosql.md)。  
  
    可以通过以下方式之一执行此操作：  
  
    -   保存脚本，然后在运行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
    -   同步数据库对象。  
  
8.  [将数据迁移到 SQL Server](migrating-oracle-data-into-sql-server-oracletosql.md)。  
  
9. 如有必要，更新数据库应用程序。  
  
## <a name="see-also"></a>请参阅  
[安装 SSMA for Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-oracletosql.md)  
[开始使用 SSMA for Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/getting-started-with-ssma-for-oracle-oracletosql.md)  
  
