---
title: "将 Access 数据库迁移到 SQL Server 的 Azure SQL DB |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-access
ms.custom: 
ms.date: 08/15/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- instructions, migration
- migrating databases, overview
- overview, migration process
- procedure, migration
- recommended migration process
ms.assetid: 76a3abcf-2998-4712-9490-fe8d872c89ca
caps.latest.revision: "23"
author: Shamikg
ms.author: Shamikg
manager: murato
ms.workload: On Demand
ms.openlocfilehash: 92ab1b9e1bd128c57347f2f68b251fce4648bfe4
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="migrating-access-databases-to-sql-server---azure-sql-db-accesstosql"></a>将访问数据库迁移到 SQL Server 的 Azure SQL DB (AccessToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Migration Assistant (SSMA) 是一个工具，提供了一个全面的环境，可帮助你快速访问将数据库迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 通过使用 SSMA，你可以查看访问和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 数据库对象、 评估迁移的 Access 数据库、 访问数据库对象转换、 加载入[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，然后将数据迁移。  
  
## <a name="recommended-migration-process"></a>建议的迁移过程  
若要成功地将对象和数据迁移到的访问从[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，请按照以下步骤：  
  
1.  [创建新的 SSMA 项目](http://msdn.microsoft.com/f2d1f0b0-5394-4adb-b3f3-abd71eb68ca7)。 创建项目之后，你可以[设置项目选项](http://msdn.microsoft.com/0a7304df-2f35-4453-96ef-7ac83dea1167)，包括转换选项、 迁移选项和数据类型映射。  
  
2.  [添加 Access 数据库文件](http://msdn.microsoft.com/e944c740-4c8a-4bc1-b0ed-be57bc06dced)到项目。  
  
    你可以添加单独的文件，包括计算机或网络上找到的文件。  
  
3.  [连接到 SQL Server 的目标实例](http://msdn.microsoft.com/f84cf007-ddf1-4396-a07c-3e0729abc769)或[连接到 SQL Azure 的目标实例](http://msdn.microsoft.com/1ba0d113-dc05-4431-8689-e14a8821bafd)。  
  
    你可以连接到 SQL Server 或 SQL Azure。  
  
4.  若要自定义一个或多个访问数据库之间的映射和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 架构[映射源和目标数据库](http://msdn.microsoft.com/69bee937-7b2c-49ee-8866-7518c683fad4)。  
  
5.  （可选） 可以[创建评估报表](http://msdn.microsoft.com/8b9e23d6-da62-437a-8c05-8ad2628b9441)来确定访问数据库对象是否可以成功转换为[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。  
  
6.  [访问数据库对象转换](http://msdn.microsoft.com/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 对象定义。  
  
7.  [将转换后的数据库对象加载到 SQL Server](http://msdn.microsoft.com/4e854eee-b10c-4f0b-9d9e-d92416e6f2ba)。  
  
    你可以加载到的数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或通过使用 SSMA，或你的 SQL Azure 可以保存[!INCLUDE[tsql](../../includes/tsql_md.md)]脚本。  
  
8.  [将访问数据迁移到 SQL Server](http://msdn.microsoft.com/f3b18af7-1af0-499d-a00d-a0af94895625)。  
  
    > [!NOTE]  
    > 你可以将转换、 加载和迁移架构和数据在一个步骤。 若要执行一次单击迁移，请单击**转换、 加载和迁移**按钮。  
  
9. 如果你希望你访问的应用程序使用中的数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，使用[Access 表链接到 SQL Server 表](http://msdn.microsoft.com/82374ad2-7737-4164-a489-13261ba393d4)。  
  
迁移向导还可用于指导你完成此过程。 有关详细信息，请参阅[迁移向导](http://msdn.microsoft.com/5bab5914-b2ae-4795-8cf5-83e42d64bef2)。  
  
## <a name="see-also"></a>另请参阅  
[Getting Started with SQL Server Migration Assistant 用于访问](http://msdn.microsoft.com/462a731f-08f1-44e1-9eeb-4deac6d2f6c5)  
[为迁移准备的 Access 数据库](http://msdn.microsoft.com/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)
