---
title: "迁移的 Oracle 数据库移到 SQL Server (OracleToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1d196dd6-4322-4c98-bb72-602c57d96134
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e4d283fe3329fb7d2a656720e9e6b72583a95f6b
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="migrating-oracle-databases-to-sql-server-oracletosql"></a>将 Oracle 数据库迁移到 SQL Server (OracleToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Migration Assistant (SSMA) 适用于 Oracle 是一个全面的环境，可帮助你快速迁移到的 Oracle 数据库[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB。 通过用于 Oracle SSMA，可以查看数据库对象和数据、 评估迁移的数据库，迁移到的数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB，然后将数据迁移到和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB。 请注意你无法迁移架构 SYS 和系统 Oracle 架构。  
  
## <a name="recommended-migration-process"></a>建议迁移过程  
若要将对象和数据成功迁移从 Oracle 数据库到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB，使用以下过程：  
  
1.  [创建新的 SSMA 项目](http://msdn.microsoft.com/en-us/ee5d94c0-c7a6-4779-bd32-729bdaf61e1b)。  
  
    创建项目后，你可以设置项目转换、 迁移和类型映射选项。 有关项目设置的信息，请参阅[设置项目选项 &#40; OracleToSQL &#41;](../../ssma/oracle/setting-project-options-oracletosql.md)。 有关如何自定义数据类型映射的信息，请参阅[映射 Oracle 和 SQL Server 数据类型 &#40; OracleToSQL &#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md)。  
  
2.  [连接到 Oracle 数据库服务器](http://msdn.microsoft.com/en-us/e276cdbf-3ebc-4ba8-b40d-a7a42befa2b6)。  
  
3.  [连接到的 SQL Server 实例](http://msdn.microsoft.com/en-us/1b2a8059-1829-4904-a82f-9c06de1e245f)。  
  
4.  [将 Oracle 数据库架构映射到 SQL Server 数据库架构](http://msdn.microsoft.com/en-us/0edeaa08-9c5d-4e3a-bc15-b9a1f0c8a9dc)。  
  
5.  （可选）[创建评估报表](http://msdn.microsoft.com/en-us/4de9bcf6-1346-4740-87f9-7f24a8226357)以评估转换的数据库对象，并估计转换时间。  
  
6.  [将 Oracle 数据库架构转换为 SQL Server 架构](http://msdn.microsoft.com/en-us/e021182d-31da-443d-b110-937f5db27272)。  
  
7.  [将转换后的数据库对象加载到 SQL Server](http://msdn.microsoft.com/en-us/a8ae33b2-1883-4785-922b-ea0e31c0b37a)。  
  
    可以通过以下方式之一来执行此操作：  
  
    -   保存脚本，然后在运行[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
    -   同步数据库对象。  
  
8.  [将数据迁移到 SQL Server](http://msdn.microsoft.com/en-us/e23c5268-41ed-4e55-9fe7-a11376202a13)。  
  
9. 如有必要，更新数据库应用程序。  
  
## <a name="see-also"></a>另請參閱  
[安装适用于 Oracle &#40; OracleToSQL &#41; SSMA](../../ssma/oracle/installing-ssma-for-oracle-oracletosql.md)  
[Getting Started with SSMA for Oracle &#40; OracleToSQL &#41;](../../ssma/oracle/getting-started-with-ssma-for-oracle-oracletosql.md)  
  

