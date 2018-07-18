---
title: 迁移的 Oracle 数据库移到 SQL Server (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 04/22/2018
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 1d196dd6-4322-4c98-bb72-602c57d96134
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: f20b7271932cbbcc0538fc9923e45b2fc029f646
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2018
ms.locfileid: "38983199"
---
# <a name="migrating-oracle-databases-to-sql-server-oracletosql"></a>Oracle 数据库迁移到 SQL Server (OracleToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 迁移助手 (SSMA) for Oracle 是一个全面的环境，可帮助你快速迁移到的 Oracle 数据库[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，Azure SQL DB 或 Azure SQL 数据仓库。 通过使用 SSMA for Oracle，可以查看数据库对象和数据、 评估要迁移的数据库，迁移到的数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，Azure SQL DB 或 Azure SQL 数据仓库，然后将数据迁移到和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，Azure SQL DB 或 Azure SQL 数据仓库。 请注意，不能将 SYS 和系统 Oracle 架构迁移。
  
## <a name="recommended-migration-process"></a>建议的迁移过程  
为了成功将对象和数据迁移到的 Oracle 数据库从[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，Azure SQL DB 或 Azure SQL 数据仓库中，使用以下过程：
  
1.  [创建新的 SSMA 项目](http://msdn.microsoft.com/ee5d94c0-c7a6-4779-bd32-729bdaf61e1b)。  
  
    创建项目后，可以设置项目转换、 迁移和类型映射选项。 有关项目设置的信息，请参阅[设置项目选项&#40;OracleToSQL&#41;](../../ssma/oracle/setting-project-options-oracletosql.md)。 有关如何自定义数据类型映射的信息，请参阅[映射 Oracle 和 SQL Server 数据类型&#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md)。  
  
2.  [连接到 Oracle 数据库服务器](http://msdn.microsoft.com/e276cdbf-3ebc-4ba8-b40d-a7a42befa2b6)。  
  
3.  [连接到 SQL server 实例](http://msdn.microsoft.com/1b2a8059-1829-4904-a82f-9c06de1e245f)。  
  
4.  [将 Oracle 数据库架构映射到 SQL Server 数据库架构](http://msdn.microsoft.com/0edeaa08-9c5d-4e3a-bc15-b9a1f0c8a9dc)。  
  
5.  （可选）[创建评估报告](http://msdn.microsoft.com/4de9bcf6-1346-4740-87f9-7f24a8226357)来评估用于转换数据库对象和估计的转换时间。  
  
6.  [Oracle 数据库架构转换为 SQL Server 架构](http://msdn.microsoft.com/e021182d-31da-443d-b110-937f5db27272)。  
  
7.  [转换后的数据库对象加载到 SQL Server](http://msdn.microsoft.com/a8ae33b2-1883-4785-922b-ea0e31c0b37a)。  
  
    可以通过以下方式之一执行此操作：  
  
    -   保存脚本，然后在运行[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
    -   同步数据库对象。  
  
8.  [将数据迁移到 SQL Server](http://msdn.microsoft.com/e23c5268-41ed-4e55-9fe7-a11376202a13)。  
  
9. 如有必要，更新数据库应用程序。  
  
## <a name="see-also"></a>请参阅  
[安装 SSMA for Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-oracletosql.md)  
[开始使用 SSMA for Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/getting-started-with-ssma-for-oracle-oracletosql.md)  
  
