---
title: 项目设置 （迁移） (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Migration settings
- Project Settings dialog box, Migration
ms.assetid: 4caebc9c-8680-4b99-a8fa-89c43161c95d
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: c8cec81d0e6281ce9f57d9d689bd5dfdc2d6feb1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47738205"
---
# <a name="project-settings-migration-accesstosql"></a>项目设置 （迁移） (AccessToSQL)
迁移项目设置允许你配置如何将数据迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。  
  
迁移窗格中现已推出**项目设置**并**默认项目设置**对话框。  
  
-   使用**项目设置**对话框来设置当前项目的配置选项。 若要访问的迁移设置中，在**工具**菜单中，选择**项目设置**，单击**常规**左窗格中，并单击底部**迁移**。  
  
-   使用**默认项目设置**对话框来设置所有项目的配置选项。 若要访问的迁移设置中，在**工具**菜单中，选择**默认项目设置**，选择项目类型中的**迁移目标版本**组合框您要访问的设置，请单击**常规**的左窗格中，并单击底部**迁移**。  
  
## <a name="options"></a>选项  
**检查约束**  
指定当其将数据添加到表 SSMA 是否应检查约束。  
  
-   **默认模式**: False  
  
-   **乐观模式**: True  
  
-   **完整模式**: False  
  
**激发触发器**  
指定添加到数据时 SSMA 是否应激发插入触发器[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表。  
  
-   **默认模式**: False  
  
-   **乐观模式**: True  
  
-   **完整模式**: False  
  
**保留标识**  
指定 SSMA 时它将添加到的数据是否保留对其进行访问的标识值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果此值为 False，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]分配标识值。  
  
-   **默认模式**: True  
  
-   **乐观模式**: True  
  
-   **完整模式**: False  
  
**保留 Null**  
指定是否 SSMA 保留源数据中的 null 值时将添加到数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]无论中指定的默认值， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
-   **默认模式**: True  
  
-   **乐观模式**: False  
  
-   **完整模式**: True  
  
**表锁**  
指定时它将数据添加到表数据迁移期间，SSMA 是否锁定表。 如果值为 False，SSMA 使用行锁。  
  
-   **默认模式**: True  
  
-   **乐观模式**: True  
  
-   **完整模式**: True  
  
**替换为不受支持的日期**  
指定是否 SSMA 应纠正访问日期早于最早[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]datetime 日期 (01 1753 年 1 月)。  
  
-   若要保留当前的日期值，选择**不执行任何操作**。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日期时间列中将不接受 01 1753 年 1 月之前的日期。 如果使用较旧的日期，必须将日期时间值转换为字符值。  
  
-   若要将 01 1753 年 1 月之前的日期转换为 NULL，请选择**替换为 NULL**。  
  
-   若要将受支持的日期替换为 01 1753 年 1 月之前的日期，请选择**替换为最近的受支持的日期**。 如果此值，请选择最接近的默认情况下将为 01 1753 年 1 月选择受支持的日期。  
  
**批大小**  
在数据迁移过程中使用的批大小。 在每个批处理后都会记录事务。 默认情况下，所有方案的批大小为 10000。  
  
## <a name="see-also"></a>请参阅  
[用户界面 Reference(Access)](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)  
  
