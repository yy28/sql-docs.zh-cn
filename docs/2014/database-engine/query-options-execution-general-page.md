---
title: 查询选项执行（"常规" 页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.query.general.f1
ms.assetid: 858a0263-2f04-4692-b8bf-63e93c998ead
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: b3ecf106315fa88fdfb68599cfce71a77be975dd
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66089035"
---
# <a name="query-options-execution-general-page"></a>“查询选项”中的“执行”（“常规”页）
  使用此页可指定用于运行[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]查询的选项。 若要访问此对话框，请右键单击“查询编辑器”窗口的主体，再单击“查询选项”****。  
  
## <a name="uielement-list"></a>UIElement 列表  
 **SET ROWCOUNT**  
 默认值为 0，指示 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 在收到所有结果之前将一直等待结果。 如果希望 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 在获取指定数目的行后暂停查询，请提供一个大于 0 的值。 若要关闭此选项（以便返回所有的行），请将 SET ROWCOUNT 指定为 0。  
  
 **SET TEXTSIZE**  
 默认值为 2,147,483,647 个字节，表示 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 将针对 `text`、`ntext`、`nvarchar(max)` 和 `varchar(max)` 数据字段提供最高上限的数据。 它将不影响 XML 数据类型。 提供较小的数值，可以在存在大量值时限制结果数量。 超出指定数量的列将被截断。  
  
 **执行超时值**  
 指示在取消查询之前等待的秒数。 值 0 指示无限期的等待或无超时。  
  
 **批分隔符**  
 键入用来将 Transact-SQL 语句分隔为批的词。 默认值为 GO。  
  
 **默认情况下，在 SQLCMD 模式下打开新查询**  
 选中此复选框可在 SQLCMD 模式下打开新查询。 仅当通过 "**工具**" 菜单打开该对话框时，此复选框才可见。  
  
 选择此选项时，请记住下列限制：  
  
-   [!INCLUDE[ssDE](../includes/ssde-md.md)] 查询编辑器中的 IntelliSense 处于关闭状态。  
  
-   由于查询编辑器不能从命令行运行，因此您不能传入命令行参数（如变量）。  
  
-   由于查询编辑器无法响应操作系统提示，因此您一定要记住不要运行交互式语句。  
  
 **重置为默认值**  
 将此页上的所有值重置为原始默认值。  
  
  
