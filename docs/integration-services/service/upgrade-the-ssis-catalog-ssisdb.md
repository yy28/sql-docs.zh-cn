---
title: "升级 SSIS 目录 (SSISDB) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.dbupgradewizard.f1"
ms.assetid: 170c3dc9-f5bf-4599-ae56-d24a620f23e8
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# 升级 SSIS 目录 (SSISDB)
  当数据库早于 SQL Server 实例当前版本时，运行 SSISDB 升级向导来升级 SSIS 目录数据库 SSISDB。 当下列任一条件成立时发生。  
  
-   从旧版 SQL Server 还原数据库。  
  
-   在升级 SQL Server 实例之前，未从 AlwaysOn 可用性组中删除数据库。 这样可以防止数据库自动升级。 有关详细信息，请参阅 [Upgrading SSISDB in an availability group](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Upgrade)。  
  
 该向导只能升级本地服务器实例上的数据库。  
  
## 通过运行 SSISDB 升级向导升级 SSIS 目录 (SSISDB)  
  
1.  备份 SSIS 目录数据库 SSISDB。  
  
2.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，展开本地服务器，然后展开“Integration Services 目录” 。  
  
3.  右键单击“SSISDB”，然后选择“数据库升级”以启动 SSISDB 升级向导。  
  
     ![Launch the SSISDB upgrade wizard](../../integration-services/service/media/ssisdb-upgrade-wizard-1.png "Launch the SSISDB upgrade wizard")  
  
4.  在“选择实例”  页上，选择本地服务器上的 SQL Server 实例。  
  
    > [!IMPORTANT]  
    >  该向导只能升级本地服务器实例上的数据库。  
  
     选中复选框以指示，你已在运行此向导之前备份 SSISDB 数据库。  
  
     ![Select the server in the SSISDB Upgrade Wizard](../../integration-services/service/media/ssisdb-upgrade-wizard-2.png "Select the server in the SSISDB Upgrade Wizard")  
  
5.  选择“升级”  以升级 SSIS 目录数据库。  
  
6.  在“结果”  页上，查看结果。  
  
     ![Review the results in the SSISDB Upgrade Wizard](../../integration-services/service/media/ssisdb-upgrade-wizard-3.png "Review the results in the SSISDB Upgrade Wizard")  
  
  