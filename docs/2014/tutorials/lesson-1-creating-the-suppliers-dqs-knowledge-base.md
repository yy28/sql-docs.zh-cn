---
title: 第 1 课： 创建供应商 DQS 知识库 |Microsoft 文档
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 78825ccb-30fc-463c-8140-435532e2ecd2
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 58f787d1204cde60dee3a10fdaf587b52cf6dfa4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36138315"
---
# <a name="lesson-1-creating-the-suppliers-dqs-knowledge-base"></a>第 1 课：创建 DQS Suppliers 知识库
  在本课中，创建名为 DQS 知识库**供应商**与供应商数据有关的知识 （元数据）。 您使用该知识库执行针对输入供应商数据的清理和匹配活动。 该清理活动标识不正确/无效数据、更正不正确数据、处理更正/建议、对数据执行标准化以及用更多的信息使数据更丰富。 该匹配活动对数据进行比较并且标识数据中的类似记录（但稍有不同），以便帮助您删除数据中的重复项。  
  
 您可以使用交互式过程和计算机辅助过程来创建、生成和管理知识库。 知识库中的知识在域中维护，每个域都是您要清理和/或匹配的数据中某个数据字段特有的。  
  
 在本课程中，执行以下任务以创建**供应商**知识库：  
  
-   创建名为 DQS 知识库**供应商**。 您可以通过几种方式来创建知识库。 您可以从头开始生成知识库，基于现有知识库来生成知识库，通过导入包含预先生成和导出的知识库的 DQS 文件 (.dqs) 来生成知识库，或者通过对示例数据执行知识发现活动来生成知识库。 在本教程中，您是从头开始创建知识库的。  
  
-   新建域**供应商**您对清理数据，和匹配数据来标识重复的知识库。 针对您要用于清理和匹配活动的数据字段创建域，而不要针对数据中的所有数据字段创建域。  
  
-   通过以下方法向域中添加值：手动添加值，从某一 Excel 文件中导入值，通过对示例数据执行知识发现活动，以及通过从某一清理项目导入项目值。 还可以通过导入包含域属性和值的 DQS 文件来导入域值，但在本教程中不执行此方法。  
  
-   设置域规则。 域规则是 DQS 用于验证、更正和标准化域值的条件。  
  
-   为域设置基于字词的关系。 通过基于字词的关系，您可以对域中作为值的一部分的字词进行更正。 例如，在值**Contoso Inc.，Inc.** 是可定义为 Incorporated 的术语。 这将有助于对数据执行标准化，以及有助于标识重复项。 例如， **Contoso Inc.** 和**Contoso Incorporated**就被认为是重复项。  
  
-   指定域值中的同义词。 您可以将两个或更多的值设置为同义词，并且将其中一个值设置为前导值，在清理活动期间，该前导值将替换其同义词值以便对数据执行标准化。  
  
-   创建名为“地址验证”的一个复合域，该域由 Address line、City、State 和 Zip 域构成。 复合域是由一个或多个单一域构成的一种域。 复合域允许您创建涉及多个域的规则。 例如，可以定义以下规则：如果 City 为 Los Angeles，则 State 必须为 CA，其中 City 和 State 是两个单独的域。  
  
-   配置和使用引用数据服务。 通过 Data Quality Services (DQS) 中的“引用数据服务”功能，您可以订阅第三方引用数据提供程序，通过对照其高质量数据进行验证以轻松地清理和丰富您的业务数据。 您可以使用 DQS 内领先的 DQS 提供程序的服务在清理过程中对数据执行标准化、更正数据或使数据更为丰富。 在本教程中，您将学习如何配置 DQS 环境以便在 Microsoft Azure 市场上使用引用数据服务，以及学习如何使用与“地址验证”复合域相关联的服务来清理地址数据。  
  
-   发布该知识库以便可以在清理和匹配活动中使用该知识库。  
  
## <a name="next-step"></a>下一步  
 [任务 1：创建知识库和域](../../2014/tutorials/task-1-creating-a-knowledge-base-and-domains.md)  
  
  