---
title: 项目设置 （加载系统对象） (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9a545233-1b0a-488a-a1ec-c33aa608dcc1
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 65f9070aabc6f64e1fc327abe67e595696c04423
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63266463"
---
# <a name="project-settingsloading-system-objects-db2tosql"></a>项目设置 （加载系统对象） (DB2ToSQL)
正在加载系统对象页**项目设置**对话框可以指定的 DB2 系统对象 SSMA 将转换并将加载到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
加载系统对象窗格中现已推出**项目设置**并**默认项目设置**对话框：  
  
-   若要指定所有的 SSMA 项目的设置**工具**菜单中，选择**默认项目设置**，选择迁移项目类型设置为其所需查看或更改从**迁移目标版本**下拉列表单击**常规**底部的左窗格中，然后单击**加载系统对象**。  
  
-   若要在指定的当前项目中，设置**工具**菜单中，选择**项目设置**，单击**常规**底部的左窗格中，然后单击**加载系统对象**。  
  
## <a name="default-settings"></a>默认设置  
将转换的系统对象会占用系统资源，需要一些时间。 若要提高性能，SSMA 仅选择的使用频率最高的系统对象，如下面的列表中所示：  
  
-   SYS.DBMS_OUTPUT  
  
-   SYS.DBMS_PIPE  
  
-   SYS.DBMS_UTILITY  
  
-   SYS。标准  
  
-   SYS.UTL_FILE  
  
-   SYS.DBMS_LOB  
  
-   SYS.DBMS_SQL  
  
-   SYS.DBMS_SESSION  
  
如果您的 DB2 对象引用其他系统对象，则应选择这些对象。 如果不选择引用的 DB2 数据库对象的系统对象，SSMA 将报告转换错误。 如果你收到转换错误引起的缺少的系统对象，在此对话框中选择所缺少的对象。 然后可以重复根据需要转换。  
  
