---
title: XML 输出文件格式（ssbdiagnose） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- XML output file format [ssbdiagnose]
- ssbdiagnose
ms.assetid: 3ceb991b-6f15-4504-8828-de5adf448bc5
author: stevestein
ms.author: sstein
ms.openlocfilehash: 56758f15a3bd2a71221c936a80f7455d9e1c1cd9
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85057618"
---
# <a name="xml-output-file-format-ssbdiagnose"></a>XML 输出文件格式 (ssbdiagnose)
  通过 **-XML** 开关运行 **ssbdiagnose** 实用工具时，该实用工具会将其结果输出为 XML 文件。 XML 输出文件将列出在分析 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 配置或会话时发现的标头信息和错误。 您可以编写应用程序分析或报告文件中列出的错误。 或者，您还可以在常规 XML 编辑器（如 XML Notepad）中查看该 XML 文件。  
  
 **ssbdiangose** 输出文件包含具有两种子类型的 DiagnosticInformation 根元素：  
  
-   带有标头信息的 Banner 元素。  
  
-   **ssbdiagnose**报告的每个问题对应的 Issue 元素。  
  
## <a name="diagnosticinformation-root-element"></a>DiagnosticInformation 根元素  
  
-   [DiagnosticInformation 元素 (ssbdiagnose)](diagnosticinformation-element-ssbdiagnose.md)  
  
## <a name="banner-element"></a>Banner 元素  
  
-   [Banner 元素 (ssbdiagnose)](banner-element-ssbdiagnose.md)  
  
## <a name="issue-element"></a>Issue 元素  
  
-   [Issue 元素 (ssbdiagnose)](issue-element-ssbdiagnose.md)  
  
## <a name="see-also"></a>另请参阅  
 [ssbdiagnose 实用工具 (Service Broker)](ssbdiagnose-utility-service-broker.md)  
  
  
