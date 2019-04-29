---
title: 附录-1 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Appendix
ms.assetid: 6dcfd6d5-772c-4876-aa94-a7f43c4b9d59
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 4e9e3aabd08566d65cd09242dbaf8a2041cc4ef1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63132273"
---
# <a name="appendix---1-sybasetosql"></a>附录 - 1 (SybaseToSQL)
SSMA 控制台命令行选项的快速视图：  
  
|Sl。 否。|开关|必需？|开关参数|允许的值|  
|-----------|----------|-------------|-------------------|--------------------|  
|1|-s/script|是|scriptfile|有效的 XML 文件名称。<br /><br />控制台脚本定义文件。|  
|2|-v/变量|否|variablevaluefile|有效的 XML 文件名称。<br /><br />如果未在脚本文件中使用变量，则必须指定此文件。|  
|3|-c/serverconnection|否|serverconnectionfile|有效的 XML 文件名称。<br /><br />此文件包含服务器连接信息。|  
|4|-x/xmloutput|否|xmloutputfile|此选项指示以 XML 格式的控制台输出。 如果未指定此选项，默认输出的文本格式。<br /><br />如果未指定 xmloutputfile，XML 输出定向到 STDOUT。<br /><br />Xmloutputfile 是文件的以 XML 格式，控制台输出写入到的名称。|  
|5|-l/log|否|logfile|有效的文件名。|  
|6|-e/projectenvironment|否|projectenvironmentfolder|有效的文件夹名称包含 SSMA 项目环境文件。|  
|7|-p/securepassword|否|-a/add {<server_id> [,...n] &#124; all} -c&#124;serverconnection  <server-connection-file> [-v&#124;variable <variable-value-file>] [-o/overwrite]<br /><br />或<br /><br />-a/add {<server_id> [,...n] &#124; all} -s&#124;script <script-file> [-v&#124;variable <variable-value-file>] [-o/overwrite]<br /><br />-r/remove {<server_id> [, ...n] &#124; all}<br /><br />-l/list<br /><br />-e/export {<server-id> [, ...n] &#124; all} <encrypted-password -file><br /><br />-i/import {<server-id> [, ...n] &#124; all} <encrypted-password-file>|如果指定，此选项不能结合任何其他选项配合使用。<br /><br />服务器 id:为 {string} 的服务器提供唯一 ID<br /><br />服务器连接文件： 服务器定义文件 （serverconnectionfile 或脚本文件）。<br /><br />变量值文件：它是一个变量定义文件，并使用服务器连接文件中。<br /><br />加密密码的文件：它是使用用户指定通行短语加密的服务器的密码文件。|  
|8|-?|否|不适用|不适用|  
  
## <a name="see-also"></a>请参阅  
[执行 SSMA 控制台 (Sybase)](https://msdn.microsoft.com/ea8950b7-fabc-4aa4-89f8-9573a2617d70)  
  
