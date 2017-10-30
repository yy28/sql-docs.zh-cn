---
title: "项目设置 （迁移） (AccessToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Migration settings
- Project Settings dialog box, Migration
ms.assetid: 4caebc9c-8680-4b99-a8fa-89c43161c95d
caps.latest.revision: 14
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3faaf19a1c591628ef97c4fe33fa0a54d4b077d5
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="project-settings-migration-accesstosql"></a>项目设置 （迁移） (AccessToSQL)
迁移项目设置允许你配置如何将数据迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。  
  
迁移窗格位于**项目设置**和**默认项目设置**对话框。  
  
-   使用**项目设置**对话框可设置为当前项目的配置选项。 若要访问的迁移设置中，在**工具**菜单上，选择**项目设置**，单击**常规**中左窗格中，然后单击底部**迁移**。  
  
-   使用**默认项目设置**对话框中设置的所有项目的配置选项。 若要访问的迁移设置中，在**工具**菜单上，选择**默认项目设置**，选择项目类型中的**迁移目标版本**你想要访问设置，请单击其中的组合框**常规**中左窗格中，然后单击底部**迁移**。  
  
## <a name="options"></a>选项  
**检查约束**  
指定是否将数据添加到表时，SSMA 应检查约束。  
  
-   **默认模式**: False  
  
-   **开放式模式**: True  
  
-   **完整模式**: False  
  
**激发触发器**  
指定将添加到的数据时，SSMA 是否应激发插入触发器[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]表。  
  
-   **默认模式**: False  
  
-   **开放式模式**: True  
  
-   **完整模式**: False  
  
**保留标识**  
指定将添加到的数据时，SSMA 是否保留访问标识值[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 如果此值为 False，[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]分配标识值。  
  
-   **默认模式**: True  
  
-   **开放式模式**: True  
  
-   **完整模式**: False  
  
**保留 Null**  
指定将添加到的数据时，SSMA 是否保留源数据中的 null 值[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]无论中指定的默认值， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
-   **默认模式**: True  
  
-   **开放式模式**: False  
  
-   **完整模式**: True  
  
**表锁**  
指定当它将添加数据到表数据迁移期间，SSMA 是否锁定表。 如果值为 False，SSMA 使用行锁。  
  
-   **默认模式**: True  
  
-   **开放式模式**: True  
  
-   **完整模式**: True  
  
**替换不受支持的日期**  
指定是否 SSMA 应更正早于最早的访问日期[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]日期日期 (01 1753 年 1 月)。  
  
-   若要保留当前的日期值，选择**不执行任何操作**。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]datetime 列中将不接受 01 1753 年 1 月之前的日期。 如果你使用较旧的日期，你必须将日期时间值转换为字符值。  
  
-   若要将 01 1753 年 1 月之前的日期转换为 NULL，选择**替换 NULL**。  
  
-   若要将替换受支持的日期 01 1753 年 1 月之前的日期，请选择**替换最受支持的日期接近**。 如果最接近默认情况下选择此值将作为 01 1753 年 1 月选择支持的日期。  
  
**批大小**  
数据迁移期间使用的批大小。 在每个批后，将记录事务。 默认情况下，所有方案的批处理大小为 10000。  
  
## <a name="see-also"></a>另请参阅  
[用户界面 Reference(Access)](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)  
  

