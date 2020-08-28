---
description: 附录 C：在开发环境中用 ADO 编程
title: 附录 C：用 ADO 编程 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, programming
ms.assetid: 40af6e70-2a37-480f-aadc-92095d450af7
author: rothja
ms.author: jroth
ms.openlocfilehash: 63240be1e7e0b9c439f39ee93f09552d4d708caa
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991148"
---
# <a name="appendix-c-programming-with-ado-in-development-environments"></a>附录 C：在开发环境中用 ADO 编程
ADO 是可与许多编程语言（包括 Microsoft Visual Basic、VBScript、JScript 和 Visual C++）结合使用的 COM 自动化接口组件。 其中的每个工具和其他应用程序（如 Microsoft Office 和 Microsoft SQL Server）都安装了 ADO 版本。

 ADO 的库是 msado15.dll 的，程序 ID (ProgID) 前缀为 "ADODB.RECORDSET"。 例如，若要显式引用 ADO [记录集](../../reference/ado-api/recordset-object-ado.md)，请使用 `ADODB.Recordset` 。

 有关在各种开发环境中用 ADO 进行编程的详细信息，请参阅以下主题：

-   [配合使用 ADO 与 Microsoft Visual Basic](./using-ado-with-microsoft-visual-basic.md)

-   [配合使用 ADO 与脚本语言](./using-ado-with-scripting-languages.md)

-   [配合使用 ADO 与 Microsoft Visual C++](./using-ado-with-microsoft-visual-c.md)

## <a name="see-also"></a>另请参阅
 [ADO API 参考](../../reference/ado-api/ado-api-reference.md)[附录 D： ADO 示例](./appendix-d-ado-samples.md)[配置 RDS](../remote-data-service/configuring-rds.md) [Microsoft ActiveX 数据对象 (ado) ](../../microsoft-activex-data-objects-ado.md) [附录 A：提供方](./appendix-a-providers.md) [ADO 历史记录](../ado-history.md)