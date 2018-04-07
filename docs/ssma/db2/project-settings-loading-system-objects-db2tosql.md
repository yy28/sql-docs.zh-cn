---
title: 项目设置 （加载系统对象） (DB2ToSQL) |Microsoft 文档
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-db2
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 9a545233-1b0a-488a-a1ec-c33aa608dcc1
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f0ec81e97380007724ba1cfeb9ee2580ca64edd0
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="project-settingsloading-system-objects-db2tosql"></a>项目设置 （加载系统对象） (DB2ToSQL)
加载系统对象页**项目设置**对话框中，可以指定哪些 DB2 系统对象 SSMA 将转换并向其中加载[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
加载系统对象窗格位于**项目设置**和**默认项目设置**对话框：  
  
-   若要对指定的所有的 SSMA 项目设置**工具**菜单上，选择**默认项目设置**，选择为其设置所需查看或更改，不再是迁移项目类型**迁移目标版本**下拉单击**常规**中左窗格中，然后单击底部**加载系统对象**。  
  
-   若要对指定为当前项目中，设置**工具**菜单上，选择**项目设置**，单击**常规**中左窗格中，然后单击底部**加载系统对象**。  
  
## <a name="default-settings"></a>默认设置  
转换系统对象占用系统资源，需要时间。 为了提高性能，SSMA 选择仅使用频率最高的系统对象，如下面的列表中所示：  
  
-   SYS.DBMS_OUTPUT  
  
-   SYS.DBMS_PIPE  
  
-   SYS.DBMS_UTILITY  
  
-   SYS.STANDARD  
  
-   SYS.UTL_FILE  
  
-   SYS.DBMS_LOB  
  
-   SYS.DBMS_SQL  
  
-   SYS.DBMS_SESSION  
  
如果您 DB2 的对象引用其他系统对象，则应选择这些对象。 如果不选择引用的 DB2 数据库对象的系统对象，SSMA 将报告转换错误。 如果你收到引起缺少系统对象的转换错误，请在此对话框中选择所缺少的对象。 然后，可以重复根据需要转换。  
  
