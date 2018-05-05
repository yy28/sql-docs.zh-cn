---
title: 迁移 DB2 数据库移到 SQL Server (DB2ToSQL) |Microsoft 文档
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-db2
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
ms.assetid: 14d2e655-af7e-4aa5-ba28-0e3d0d025518
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: fbc4823fc61b3678b29ac5e0fee482384605abc8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="migrating-db2-databases-to-sql-server-db2tosql"></a>将 DB2 数据库迁移到 SQL Server (DB2ToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant (SSMA) for DB2 是一个全面的环境，可帮助你快速迁移到 DB2 数据库[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB。 通过使用 SSMA for DB2，可以查看数据库对象和数据、 评估迁移的数据库，迁移到的数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB，然后将数据迁移到和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB。 请注意你无法迁移架构 SYS 和系统 DB2 架构。  
  
## <a name="recommended-migration-process"></a>建议迁移过程  
若要将对象和数据成功迁移从 DB2 数据库到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB，使用以下过程：  
  
1.  [新的 SSMA 项目](http://msdn.microsoft.com/en-us/66437b45-4686-4fc7-a91b-ebde45e0f1b0)。  
  
    创建项目后，你可以设置项目转换、 迁移和类型映射选项。 有关项目设置的信息，请参阅[项目设置&#40;转换&#41; &#40;DB2ToSQL&#41; ](../../ssma/db2/project-settings-conversion-db2tosql.md)和相关部分。 有关如何自定义数据类型映射的信息，请参阅[映射 DB2 和 SQL Server 数据类型&#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md)。  
  
2.  [连接到 DB2 数据库](http://msdn.microsoft.com/en-us/5eb5801d-f0c3-4127-97c0-0b1ef49f4844)。  
  
3.  [连接到 SQL Server](http://msdn.microsoft.com/en-us/b59803cb-3cc6-41cc-8553-faf90851410e)。  
  
4.  [将 DB2 架构映射到 SQL Server 架构](http://msdn.microsoft.com/en-us/05ff7bd4-e60b-4f48-a893-bc2346aa9a8a)。  
  
5.  （可选）[评估报表](http://msdn.microsoft.com/en-us/9e13eba0-e3cf-4205-974f-c00f982061de)以评估转换的数据库对象，并估计转换时间。  
  
6.  [转换 DB2 架构](http://msdn.microsoft.com/en-us/7947efc3-ca86-4ec5-87ce-7603059c75a0)。  
  
7.  [将转换后的数据库对象加载到 SQL Server](http://msdn.microsoft.com/en-us/f4ea1ced-9f9f-4a9d-88ab-81dbab64adc3)。  
  
    可以通过以下方式之一来执行此操作：  
  
    -   保存脚本，然后在运行[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
    -   同步数据库对象。  
  
8.  [将 DB2 数据迁移到 SQL Server](http://msdn.microsoft.com/en-us/86cbd39f-6dac-409a-9ce1-7dd54403f84b)。  
  
9. 如有必要，更新数据库应用程序。  
  
## <a name="see-also"></a>另请参阅  
[安装适用于 DB2 SSMA &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-db2tosql.md)  
[入门 DB2 SSMA &#40;DB2ToSQL&#41;](../../ssma/db2/getting-started-with-ssma-for-db2-db2tosql.md)  
  
