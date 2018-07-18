---
title: OLE DB 命令转换 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.oledbcommandtrans.f1
helpviewer_keywords:
- statements [Integration Services]
- OLE DB Command transformation
ms.assetid: baa6735c-5acf-4759-b077-1216aca16c6c
caps.latest.revision: 55
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5424c163c21d6161cbb6a584ba224815a0c70daa
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37162958"
---
# <a name="ole-db-command-transformation"></a>OLE DB 命令转换
  OLE DB 命令转换对数据流中的每一行运行一条 SQL 语句。 例如，您可以运行 SQL 语句以在数据库表中插入、更新或删除行。  
  
 可以按下列方式配置 OLE DB 命令转换：  
  
-   提供转换为每一行所运行的 SQL 语句。  
  
-   指定一个秒数，到此秒数该 SQL 语句即告超时。  
  
-   指定默认的代码页。  
  
 通常，所运行的 SQL 语句会包含一些参数。 参数值存储在转换输入的外部列中，将输入列映射到外部列便可将输入列映射到参数。 例如，若要按 **ProductKey** 列中的值在 **DimProduct** 表中查找行，然后删除这些行，可将名为 **Param_0** 的外部列映射到名为 **ProductKey** 的输入列，然后再运行 SQL 语句 `DELETE FROM DimProduct WHERE ProductKey = ?`。 OLE DB 命令转换提供参数的名称，这些参数名不可修改。 参数名的形式为 **Param_0**、 **Param_1**等，依此类推。  
  
 如果使用 **“高级编辑器”** 对话框配置 OLE DB 命令转换，单击 **“刷新”** 按钮便可将 SQL 语句中的参数自动映射到转换输入中的外部列，并定义每个参数的特征。 但是，如果 OLE DB 命令转换所使用的 OLE DB 访问接口不支持从参数派生参数信息，则必须手动配置外部列。 这意味着对每个参数，必须在转换的外部输入中添加一列，用类似 **Param_0**的名称更新列名，指定 DBParamInfoFlags 属性的值，并将包含参数值的输入列映射到这些外部列。  
  
 DBParamInfoFlags 的值表示参数的特征。 例如，值 **1** 指定参数为输入参数，而值 **65** 则指定参数为输入参数，且可能包含空值。 该值必须与 OLE DB DBPARAMFLAGSENUM 枚举中包含的值相匹配。 有关详细信息，请参阅 OLE DB 参考文档。  
  
 OLE DB 命令转换包括 `SQLCommand` 自定义属性。 加载包时，可以通过属性表达式更新此属性。 有关详细信息，请参阅 [Integration Services (SSIS) 表达式](../../expressions/integration-services-ssis-expressions.md)、[在包中使用属性表达式](../../expressions/use-property-expressions-in-packages.md)和[转换自定义属性](transformation-custom-properties.md)。  
  
 此转换有一个输入、一个常规输出和一个错误输出。  
  
## <a name="logging"></a>日志记录  
 可以记录 OLE DB 命令转换对外部数据访问接口所做的调用。 利用此日志记录功能，可以排除 OLE DB 命令转换对外部数据源执行的连接和命令中发生的故障。 若要记录 OLE DB 命令转换对外部数据访问接口所做的调用，请在包级别启用包日志记录并选择 **“诊断”** 事件。 有关详细信息，请参阅 [包执行的疑难解答工具](../../troubleshooting/troubleshooting-tools-for-package-execution.md)。  
  
## <a name="related-tasks"></a>Related Tasks  
 可通过使用 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器或对象模型配置转换。 有关使用 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器配置转换的详细信息，请参阅  [配置 OLE DB 命令转换](../../configure-the-ole-db-command-transformation.md)。 有关以编程方式配置此转换的详细信息，请参阅开发人员指南。  
  
## <a name="see-also"></a>请参阅  
 [数据流](../data-flow.md)   
 [Integration Services 转换](integration-services-transformations.md)  
  
  
