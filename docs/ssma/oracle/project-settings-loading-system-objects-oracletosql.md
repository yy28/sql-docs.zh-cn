---
title: 项目设置 （加载系统对象） (OracleToSQL) |Microsoft 文档
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 9418cb34-d869-4d24-95b3-6cb9db949bb0
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: e6137dafd3a1dacbd9170fa47e9b91d15927c25a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="project-settingsloading-system-objects-oracletosql"></a>项目设置 （加载系统对象） (OracleToSQL)
加载系统对象页**项目设置**对话框中，可以指定哪些 Oracle 系统对象 SSMA 将转换并向其中加载[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
加载系统对象窗格位于**项目设置**和**默认项目设置**对话框：  
  
-   若要对指定的所有的 SSMA 项目设置**工具**菜单上，选择**默认项目设置**，选择为其设置所需查看或更改，不再是迁移项目类型**迁移目标版本**下拉单击**常规**中左窗格中，然后单击底部**加载系统对象**。  
  
-   若要对指定为当前项目中，设置**工具**菜单上，选择**项目设置**，单击**常规**中左窗格中，然后单击底部**加载系统对象**。  
  
## <a name="default-settings"></a>默认设置  
转换系统对象占用系统资源，需要时间。 为了提高性能，SSMA 选择仅使用频率最高的系统对象，如下面的列表中所示：  
  
-   SYS.DBMS_OUTPUT  
  
-   SYS.DBMS_PIPE  
  
-   SYS.DBMS_UTILITY  
  
-   SYS。标准  
  
-   SYS.UTL_FILE  
  
-   SYS.DBMS_LOB  
  
-   SYS.DBMS_SQL  
  
-   SYS.DBMS_SESSION  
  
如果 Oracle 对象引用其他系统对象，则应选择这些对象。 如果不选择引用的 Oracle 数据库对象的系统对象，SSMA 将报告转换错误。 如果你收到引起缺少系统对象的转换错误，请在此对话框中选择所缺少的对象。 然后，可以重复根据需要转换。  
  
