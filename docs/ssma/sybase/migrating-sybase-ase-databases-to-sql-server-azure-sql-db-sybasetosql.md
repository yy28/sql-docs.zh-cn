---
title: "将 Sybase ASE 数据库迁移到 SQL Server 的 Azure SQL DB |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: ed7952d4-8331-44d7-bccf-3440e17238b2
caps.latest.revision: "7"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1bc6d8b076588b53d83e6af9e88be5dff14f08f4
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="migrating-sybase-ase-databases-to-sql-server---azure-sql-db-sybasetosql"></a>Sybase ASE 将数据库迁移到 SQL Server 的 Azure SQL DB (SybaseToSQL)
SQL Server 迁移助手 (SSMA) 用于 Sybase 是一个全面的环境，可帮助你快速 Sybase 自适应 Server Enterprise (ASE) 将数据库迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB。 通过用于 Sybase 的 SSMA，你可以查看数据库对象和数据、 评估迁移的数据库，迁移到的数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB，然后将数据迁移到和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB。  
  
## <a name="recommended-migration-process"></a>建议迁移过程  
若要将对象和数据成功迁移从 ASE 数据库到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB，使用以下过程：  
  
1.  [创建新的 SSMA 项目](http://msdn.microsoft.com/en-us/11091d95-c488-48c3-891a-743cac94ac93)。  
  
    创建项目后，你可以设置项目转换、 迁移和类型映射选项。 有关项目设置的信息，请参阅[设置项目选项 &#40;SybaseToSQL &#41;](../../ssma/sybase/setting-project-options-sybasetosql.md). 有关自定义数据类型映射的信息，请参阅[映射 Sybase ASE 和 SQL Server 数据类型 &#40;SybaseToSQL &#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
2.  [连接到 Sybase ASE 数据库服务器](http://msdn.microsoft.com/en-us/a45a2330-9175-4c9e-af38-ef920e350614)。  
  
3.  [连接到 SQL Server 实例](http://msdn.microsoft.com/en-us/dd368a1a-45b0-40e9-b4d3-5cdb48c26606)或[连接到的 Azure SQL DB 实例](http://msdn.microsoft.com/en-us/9e77e4b0-40c0-455c-8431-ca5d43849aa7)。  
  
4.  [将 ASE 数据库架构映射到 SQL Server / Azure SQL DB 数据库架构](http://msdn.microsoft.com/en-us/2c927003-c49d-4fe1-8e3e-5b2899166268)。  
  
5.  （可选）[创建评估报表](http://msdn.microsoft.com/en-us/eb996b7c-1eef-4f73-b5e6-2fa6faf7336c)以评估转换的数据库对象，并估计转换时间。  
  
6.  [将 Sybase ASE 数据库架构转换为 SQL Server / Azure SQL DB 架构](http://msdn.microsoft.com/en-us/509cb65d-2f54-427a-83d7-37919cc4e3e3)。  
  
7.  [将转换后的数据库对象加载到 SQL Server / Azure SQL DB](http://msdn.microsoft.com/en-us/4c59256f-99a8-4351-9559-a455813dbd06)。  
  
    你可以通过以下任一方式保存脚本，然后在运行[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB，或者你可以同步数据库对象。  
  
8.  [将数据迁移到 SQL Server / Azure SQL DB](http://msdn.microsoft.com/en-us/54a39f5e-9250-4387-a3ae-eae47c799811)。  
  
9. 如有必要，更新你的数据库应用程序。  
  
## <a name="see-also"></a>另请参阅  
[安装适用于 Sybase &#40; SSMASybaseToSQL &#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
[用于 Sybase &#40; 入门 SSMASybaseToSQL &#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)  
  
