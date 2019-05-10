---
title: 第 1 课：创建 DQS Suppliers 知识库 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 78825ccb-30fc-463c-8140-435532e2ecd2
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 6e25b57bce84876de1119ec52ad068602cd5cf13
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65485582"
---
# <a name="lesson-1-creating-the-suppliers-dqs-knowledge-base"></a>第 1 课：创建 DQS Suppliers 知识库
  在本课程中，创建名为 DQS 知识库**供应商**与供应商数据相关的知识 （元数据）。 您使用该知识库执行针对输入供应商数据的清理和匹配活动。 该清理活动标识不正确/无效数据、更正不正确数据、处理更正/建议、对数据执行标准化以及用更多的信息使数据更丰富。 该匹配活动对数据进行比较并且标识数据中的类似记录（但稍有不同），以便帮助您删除数据中的重复项。  
  
 您可以使用交互式过程和计算机辅助过程来创建、生成和管理知识库。 知识库中的知识在域中维护，每个域都是您要清理和/或匹配的数据中某个数据字段特有的。  
  
 在本课程中，执行以下任务来创建**供应商**知识库：  
  
-   创建名为 DQS 知识库**供应商**。 您可以通过几种方式来创建知识库。 您可以从头开始生成知识库，基于现有知识库来生成知识库，通过导入包含预先生成和导出的知识库的 DQS 文件 (.dqs) 来生成知识库，或者通过对示例数据执行知识发现活动来生成知识库。 在本教程中，您是从头开始创建知识库的。  
  
-   创建中的域**供应商**知识库，用于清理数据，以及匹配的数据以确定重复项。 针对您要用于清理和匹配活动的数据字段创建域，而不要针对数据中的所有数据字段创建域。  
  
-   通过以下方法向域中添加值：手动添加值，从某一 Excel 文件中导入值，通过对示例数据执行知识发现活动，以及通过从某一清理项目导入项目值。 还可以通过导入包含域属性和值的 DQS 文件来导入域值，但在本教程中不执行此方法。  
  
-   设置域规则。 域规则是 DQS 用于验证、更正和标准化域值的条件。  
  
-   为域设置基于字词的关系。 通过基于字词的关系，您可以对域中作为值的一部分的字词进行更正。 例如，在值**Contoso Inc.，Inc.** 是可以定义为 Incorporated 的字词。 这将有助于对数据执行标准化，以及有助于标识重复项。 例如， **Contoso Inc.** 并**Contoso Incorporated**可被视为重复项。  
  
-   指定域值中的同义词。 您可以将两个或更多的值设置为同义词，并且将其中一个值设置为前导值，在清理活动期间，该前导值将替换其同义词值以便对数据执行标准化。  
  
-   创建名为“地址验证”的一个复合域，该域由 Address line、City、State 和 Zip 域构成。 复合域是由一个或多个单一域构成的一种域。 复合域允许您创建涉及多个域的规则。 例如，可以定义以下规则：如果 City 为 Los Angeles，则 State 必须为 CA，其中 City 和 State 是两个单独的域。  
  
-   配置和使用引用数据服务。 通过 Data Quality Services (DQS) 中的“引用数据服务”功能，您可以订阅第三方引用数据提供程序，通过对照其高质量数据进行验证以轻松地清理和丰富您的业务数据。 您可以使用 DQS 内领先的 DQS 提供程序的服务在清理过程中对数据执行标准化、更正数据或使数据更为丰富。 在本教程中，您将学习如何配置 DQS 环境以便在 Microsoft Azure 市场上使用引用数据服务，以及学习如何使用与“地址验证”复合域相关联的服务来清理地址数据。  
  
-   发布该知识库以便可以在清理和匹配活动中使用该知识库。  
  
## <a name="next-step"></a>下一步  
 [任务 1:创建知识库和域](../../2014/tutorials/task-1-creating-a-knowledge-base-and-domains.md)  
  
  
