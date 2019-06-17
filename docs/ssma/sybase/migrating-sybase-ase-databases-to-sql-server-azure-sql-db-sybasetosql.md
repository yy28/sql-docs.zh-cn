---
title: 将 Sybase ASE 数据库迁移到 SQL Server-Azure SQL 数据库 |Microsoft Docs
ms.custom: ''
ms.date: 11/30/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ed7952d4-8331-44d7-bccf-3440e17238b2
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 96ade7125c0d03963e8e012ed72bdb8fdef492cf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62705467"
---
# <a name="migrating-sap-ase-databases-to-sql-server---azure-sql-database-sybasetosql"></a>将 SAP ASE 数据库迁移到 SQL Server-Azure SQL 数据库 (SybaseToSQL)
SQL Server Migration Assistant (SSMA) 的 SAP Adaptive Server Enterprise (ASE) 是一个全面的环境，可帮助你快速 SAP ASE 数据库迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL 数据库。 通过使用 SSMA for SAP ASE，可以查看数据库对象和数据、 评估要迁移的数据库，迁移到的数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL 数据库，然后将数据迁移到和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL 数据库。  
  
## <a name="recommended-migration-process"></a>建议的迁移过程  
为了成功将对象和数据迁移到 SAP ASE 数据库从[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL 数据库中，使用以下过程：  
  
1.  [创建新的 SSMA 项目](working-with-ssma-projects-sybasetosql.md)。  
  
    创建项目后，可以设置项目转换、 迁移和类型映射选项。 有关项目设置的信息，请参阅[设置项目选项&#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md)。 有关自定义数据类型映射的信息，请参阅[映射 Sybase ASE 和 SQL Server 数据类型&#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)。  
  
2.  [连接到 SAP ASE 数据库服务器](connecting-to-sybase-ase-sybasetosql.md)。  
  
3.  [连接到 SQL Server 实例](connecting-to-sql-server-sybasetosql.md)或[连接到 Azure SQL 数据库实例](connecting-to-azure-sql-db-sybasetosql.md)。  
  
4.  [将 SAP ASE 数据库架构映射到 SQL Server / Azure SQL 数据库数据库架构](https://msdn.microsoft.com/2c927003-c49d-4fe1-8e3e-5b2899166268)。  
  
5.  （可选）[创建评估报告](assessing-sybase-ase-database-objects-for-conversion-sybasetosql.md)来评估用于转换数据库对象和估计的转换时间。  
  
6.  [SAP ASE 数据库架构转换为 SQL Server / Azure SQL 数据库架构](https://msdn.microsoft.com/509cb65d-2f54-427a-83d7-37919cc4e3e3)。  
  
7.  [转换后的数据库对象加载到 SQL Server / Azure SQL 数据库](https://msdn.microsoft.com/4c59256f-99a8-4351-9559-a455813dbd06)。  
  
    可以保存脚本，然后在运行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL 数据库，或同步的数据库对象。  
  
8.  [将数据迁移到 SQL Server / Azure SQL 数据库](https://msdn.microsoft.com/54a39f5e-9250-4387-a3ae-eae47c799811)。  
  
9. 如有必要，更新数据库应用程序。  
  
## <a name="see-also"></a>另请参阅  
[安装 SSMA for SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
[入门 SAP ASE 的 SSMA &#40;SybaseToSQL&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)  
  
