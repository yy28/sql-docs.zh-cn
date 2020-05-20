---
title: 查询选项执行（ANSI 页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.query.ansi.f1
ms.assetid: c90d7cdf-3309-46f4-b900-220521bb9552
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1b383c290bb507cdafaf824c16b3a1587b998bd3
ms.sourcegitcommit: 4b5919e3ae5e252f8d6422e8e6fddac1319075a1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2020
ms.locfileid: "83000614"
---
# <a name="query-options-execution-ansi-page"></a>“查询选项”中的“执行”（ANSI 页）
  使用此页可以指定 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 将使用 ISO （ANSI）标准中指定的全部或部分设置运行查询。  
  
## <a name="uielement-list"></a>UIElement 列表  
 **SET ANSI_DEFAULTS**  
 选择所有默认的 ISO 设置。 默认情况下，此框不可用，因为只配置了部分 ISO 设置。  
  
 **SET QUOTED_IDENTIFIER**  
 用引号将对象标识符引起来。 默认情况下选择此选项。  
  
 **SET ANSI_NULL_DFLT_ON**  
 在 CREATE TABLE 或 ALTER TABLE 语句执行过程中，没有显式定义为 NOTNULL 的所有用户定义的数据类型或列都将默认为允许空值。 默认情况下选择此选项。  
  
 **SET IMPLICIT_TRANSACTIONS**  
 默认情况下不选择此选项。  
  
 **SET CURSOR_CLOSE_ON_COMMIT**  
 在提交事务时，自动关闭所有打开的游标（遵从 ISO 标准）。 如果清除此选项（设置为 OFF），游标将跨越事务边界始终保持打开状态，游标只有在关闭连接或显示关闭它们时才关闭。 默认情况下不选择此选项。  
  
 **SET ANSI_PADDING**  
 控制列存储小于列定义大小的值的方式，以及列存储在**char**、 **varchar**、 **binary**和**varbinary**数据中具有尾随空格的值的方式。 此设置只影响新列的定义。 创建列后， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 会基于创建列时的设置存储这些值。 以后对此设置的更改不会影响现有的列。 默认情况下，此复选框为选中状态。  
  
 **SET ANSI_WARNINGS**  
 指定对几种错误条件采用 ISO 标准行为：  
  
-   选中此复选框后，如果在聚合函数（如 SUM、AVG、MAX、MIN、STDEV、STDEVP、VAR、VARP 或 COUNT）中出现了空值，则会生成一条警告消息。 当为**OFF**时，不发出警告。  
  
-   如果清除此复选框，则在发生被零除错误和算术溢出错误时，将导致语句回滚并生成一条错误信息。 如果设置为 OFF，则在发生被零除错误和算术溢出错误时，将导致返回空值。 如果尝试对 character、Unicode 或 binary 列执行 INSERT 或 UPDATE 操作，而这些列中的新值长度超出列的最大大小，那么，在发生被零除错误或算术溢出错误时，将导致返回空值。 如果**SET ANSI_WARNINGS**为 ON，则根据 ISO 标准的指定取消插入或更新操作。 字符列的尾随空格和二进制列的尾随零都将被忽略。 设置为 OFF 时，数据将剪裁为列的大小，并且语句执行成功。  
  
 默认情况下选择此选项。  
  
 **SET ANSI_NULLS**  
 指定在与 Null 值一起使用等于 (`=`) 和不等于 (`<>`) 比较运算符时采用符合 ISO 标准的行为。 当选中 **SET ANSI_NULLS** 时，所有与 Null 值进行比较求得的值均为 UNKNOWN，这是符合 ISO 标准的行为。 如果未选中 **SET ANSI_NULLS** ，则在数据值为 NULL 时，所有数据与空值的比较求得的值为 TRUE。 默认情况下选择此选项。  
  
 **重置为默认值**  
 将此页上的所有值重置为原始默认值。  
  
  
