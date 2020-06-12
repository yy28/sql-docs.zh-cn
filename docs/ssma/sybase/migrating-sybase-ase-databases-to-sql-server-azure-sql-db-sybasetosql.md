---
title: 将 Sybase ASE 数据库迁移到 SQL Server-Azure SQL 数据库 |Microsoft Docs
description: 使用此建议过程将 SAP 自适应服务器企业数据库迁移到使用 SQL Server 迁移助手的 SQL Server 或 Azure SQL 数据库（SSMA）。
ms.custom: ''
ms.date: 11/30/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ed7952d4-8331-44d7-bccf-3440e17238b2
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: a9bcca5d23fe147394a350ff8c640680ec674675
ms.sourcegitcommit: 59cda5a481cfdb4268b2744edc341172e53dede4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2020
ms.locfileid: "84292814"
---
# <a name="migrating-sap-ase-databases-to-sql-server---azure-sql-database-sybasetosql"></a>将 SAP ASE 数据库迁移到 SQL Server-Azure SQL 数据库（SybaseToSQL）
适用于 SAP 自适应服务器企业（ASE）的 SQL Server 迁移助手（SSMA）是一个全面的环境，可帮助你快速将 SAP ASE 数据库迁移到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 AZURE SQL 数据库。 通过使用 SSMA for SAP ASE，你可以查看数据库对象和数据、评估要迁移的数据库、将数据库对象迁移到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 AZURE Sql 数据库，以及将数据迁移到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure sql 数据库。  
  
## <a name="recommended-migration-process"></a>建议的迁移过程  
若要成功地将对象和数据从 SAP ASE 数据库迁移到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 AZURE SQL 数据库，请使用以下过程：  
  
1.  [创建新的 SSMA 项目](working-with-ssma-projects-sybasetosql.md)。  
  
    创建项目后，可以设置项目转换、迁移和类型映射选项。 有关项目设置的信息，请参阅[设置项目选项 &#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md)。 有关自定义数据类型映射的信息，请参阅将[SYBASE ASE 和 SQL Server 数据类型映射 &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)。  
  
2.  [连接到 SAP ASE 数据库服务器](connecting-to-sybase-ase-sybasetosql.md)。  
  
3.  [连接到实例 SQL Server](connecting-to-sql-server-sybasetosql.md)或[连接到 Azure SQL 数据库的实例](connecting-to-azure-sql-db-sybasetosql.md)。  
  
4.  [将 SAP ASE 数据库架构映射到 SQL Server/AZURE SQL 数据库数据库架构](https://msdn.microsoft.com/2c927003-c49d-4fe1-8e3e-5b2899166268)。  
  
5.  （可选）[创建评估报表](assessing-sybase-ase-database-objects-for-conversion-sybasetosql.md)以评估用于转换的数据库对象，并估计转换时间。  
  
6.  [将 SAP ASE 数据库架构转换为 SQL Server/AZURE SQL 数据库架构](https://msdn.microsoft.com/509cb65d-2f54-427a-83d7-37919cc4e3e3)。  
  
7.  [将转换后的数据库对象加载到 SQL Server/AZURE SQL 数据库中](https://msdn.microsoft.com/4c59256f-99a8-4351-9559-a455813dbd06)。  
  
    保存脚本并在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 AZURE SQL 数据库中运行该脚本，或者同步数据库对象。  
  
8.  [将数据迁移到 SQL Server/AZURE SQL 数据库](https://msdn.microsoft.com/54a39f5e-9250-4387-a3ae-eae47c799811)。  
  
9. 如有必要，请更新数据库应用程序。  
  
## <a name="see-also"></a>另请参阅  
[安装 SSMA for SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
[SSMA for SAP ASE &#40;SybaseToSQL&#41;的入门](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)  
  
