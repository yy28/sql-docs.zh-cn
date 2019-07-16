---
title: 项目设置 （转换） (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- conversion, options described
- Project Settings dialog box, Conversion
ms.assetid: bcebc635-c638-4ddb-924c-b9ccfef86388
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: ff44d34e6c701c8d43260982d3117def4cb9530d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67929456"
---
# <a name="project-settings-conversion-accesstosql"></a>项目设置 （转换） (AccessToSQL)
转换项目设置允许你配置如何将对象转换到访问数据库对象从[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 数据库对象。  
  
转换窗格中现已推出**项目设置**并**默认项目设置**对话框。  
  
-   使用**项目设置**对话框来设置当前项目的配置选项。 若要访问的转换设置中，在**工具**菜单中，选择**项目设置**，单击**常规**在左窗格中，并选择底部**转换**。  
  
-   使用**默认项目设置**对话框来设置所有项目的配置选项。 若要访问的转换设置中，在**工具**菜单中，选择**默认项目设置**，选择迁移项目类型设置为其所需查看 / 更改从**迁移目标版本**下拉列表中，单击**常规**在左窗格中，并选择底部**转换**。  
  
## <a name="options"></a>选项  
**添加主键**  
创建新的主密钥中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 表，如果访问表没有主键或唯一索引。  
  
-   **默认模式**:False  
  
-   **乐观模式**:False  
  
-   **完整模式**:True  
  
连接到 SQL Azure 时，它是默认情况下 True。**添加时间戳列**  
指定是否需要 SSMA 是否应创建一个时间戳值。  
  
-   **默认模式**:让决定的 SSMA  
  
-   **乐观模式**:从不  
  
-   **完整模式**:让决定的 SSMA  
  
**包括转换评估报告使用的数据评估报表**  
评估报表中包括数据评估。  
  
-   **默认模式**:True  
  
-   **乐观模式**:False  
  
-   **完整模式**:True  
  
**如果主键包含为 null 的列的消息类型**  
指定的 SSMA 显示了输出窗格中，找到主键为 null 的列时的消息 （警告、 错误或执行任何操作） 的类型。  
  
-   **默认模式**:警告  
  
-   **乐观模式**:没有消息  
  
-   **完整模式**:Error  
  
**当外键列具有不同大小的消息类型**  
指定的 SSMA 显示了输出窗格中，找到不正确的文本外键时的消息 （警告、 错误或执行任何操作） 的类型。  
  
-   **默认模式**:警告  
  
-   **乐观模式**:没有消息  
  
-   **完整模式**:Error  
  
**Memo 列编制索引时的消息类型**  
指定的 SSMA 显示了输出窗格中，找到包含的索引时的消息 （警告、 错误或执行任何操作） 的类型**memo**列。  
  
-   **默认模式**:警告  
  
-   **乐观模式**:没有消息  
  
-   **完整模式**:Error  
  
**当一个复杂的查询使用通配符，则发出警告 (\&#42;)**  
SELECT 语句中的列名为通配符 （*） 时，将输出窗格和错误列表中显示警告。  
  
-   **默认模式**:True  
  
-   **乐观模式**:False  
  
-   **完整模式**:True  
  
**标识符名称发生更改时，则发出警告**  
SSMA 更改的对象标识符名称时，在评估报表并在输出窗格中显示一条消息。  
  
-   **默认模式**:True  
  
-   **乐观模式**:False  
  
-   **完整模式**:True  
  
**将带引号的标识符时发出警告**  
对象标识符名称将带引号的 SSMA 时，在评估报表并在输出窗格中显示一条消息。 名称是一个关键字，或包含特殊字符时是必需的标识符引起来。  
  
-   **默认模式**:True  
  
-   **乐观模式**:False  
  
-   **完整模式**:True  
  
## <a name="see-also"></a>请参阅  
[用户界面 Reference(Access)](https://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
