---
title: "项目设置 （转换） (AccessToSQL) |Microsoft 文档"
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
- conversion, options described
- Project Settings dialog box, Conversion
ms.assetid: bcebc635-c638-4ddb-924c-b9ccfef86388
caps.latest.revision: 16
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: c9a9c7fb027bfd8f90d5310bb096eaef706aa353
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="project-settings-conversion-accesstosql"></a>项目设置 （转换） (AccessToSQL)
转换项目设置允许你配置如何将对象转换到的访问数据库对象从[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 数据库对象。  
  
转换窗格位于**项目设置**和**默认项目设置**对话框。  
  
-   使用**项目设置**对话框可设置为当前项目的配置选项。 若要访问的转换设置中，在**工具**菜单上，选择**项目设置**，单击**常规**底部的左窗格中，，然后选择**转换**。  
  
-   使用**默认项目设置**对话框中设置的所有项目的配置选项。 若要访问的转换设置中，在**工具**菜单上，选择**默认项目设置**，选择为其设置所需查看 / 更改，不再是迁移项目类型**迁移目标版本**下拉列表中，单击**常规**底部的左窗格中，，然后选择**转换**。  
  
## <a name="options"></a>选项  
**添加主键**  
创建中的新主键[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 表，如果访问表没有主键或唯一索引。  
  
-   **默认模式**: False  
  
-   **开放式模式**: False  
  
-   **完整模式**: True  
  
当连接到 SQL Azure，它是默认情况下，True。**添加时间戳列**  
指定是否需要 SSMA 是否应创建时间戳值。  
  
-   **默认模式**： 让 SSMA 决定  
  
-   **开放式模式**： 永远不会  
  
-   **完整模式**： 让 SSMA 决定  
  
**包括具有转换评估报表的数据评估报表**  
评估报表中包括数据评估。  
  
-   **默认模式**: True  
  
-   **开放式模式**: False  
  
-   **完整模式**: True  
  
**如果主键包含 null 的列的消息类型**  
指定当它找到为 null 的列的主键，SSMA 输出窗格中显示的消息 （警告、 错误或执行任何操作） 的类型。  
  
-   **默认模式**： 警告  
  
-   **开放式模式**： 任何消息  
  
-   **完整模式**： 错误  
  
**消息类型外键列时的不同的大小**  
指定当它发现不正确的文本外键时，SSMA 输出窗格中显示的消息 （警告、 错误或执行任何操作） 的类型。  
  
-   **默认模式**： 警告  
  
-   **开放式模式**： 任何消息  
  
-   **完整模式**： 错误  
  
**消息类型时 memo 列编制索引**  
指定当它找到包含索引 SSMA 输出窗格中显示的消息 （警告、 错误或执行任何操作） 的类型**备注**列。  
  
-   **默认模式**： 警告  
  
-   **开放式模式**： 任何消息  
  
-   **完整模式**： 错误  
  
**在复杂查询使用通配符，则发出警告 (\&#42;)**  
SELECT 语句中的列名为通配符 （*） 时，请在输出窗格和错误列表中显示警告。  
  
-   **默认模式**: True  
  
-   **开放式模式**: False  
  
-   **完整模式**: True  
  
**标识符名称发生更改时，则发出警告**  
SSMA 更改对象标识符名称时，在评估的报表并在输出窗格中显示一条消息。  
  
-   **默认模式**: True  
  
-   **开放式模式**: False  
  
-   **完整模式**: True  
  
**当将带引号的标识符，则发出警告**  
在对象标识符名称将用引号引起的 SSMA 时，在评估的报表并在输出窗格中显示一条消息。 名称是一个关键字，或包含特殊字符时，用引号括起来标识符是必需的。  
  
-   **默认模式**: True  
  
-   **开放式模式**: False  
  
-   **完整模式**: True  
  
## <a name="see-also"></a>另請參閱  
[用户界面 Reference(Access)](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)  
  

