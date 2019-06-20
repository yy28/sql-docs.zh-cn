---
title: 附录-1 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: e01f8be5-ce68-4c9f-bd13-d65e73a16470
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: ad627f91cedf04c71d53bf14f8e0427aa531f3f1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63287787"
---
# <a name="appendix---1-oracletosql"></a>附录 - 1 (OracleToSQL)
SSMA 控制台命令行选项的快速视图：  
  
|Sl。 否。|开关|必需？|开关参数|允许的值|  
|-----------|----------|-------------|-------------------|--------------------|  
|1|-s/script|是|scriptfile|有效的 XML 文件名称。<br /><br />控制台脚本定义文件。|  
|2|-v/变量|否|variablevaluefile|有效的 XML 文件名称。<br /><br />如果未在脚本文件中使用变量，则必须指定此文件。|  
|3|-c/serverconnection|否|serverconnectionfile|有效的 XML 文件名称。<br /><br />此文件包含服务器连接信息。|  
|4|-x/xmloutput|否|xmloutputfile|此选项指示以 XML 格式的控制台输出。 如果未指定此选项，默认输出的文本格式。<br /><br />如果未指定 xmloutputfile，XML 输出定向到`STDOUT`。<br /><br />Xmloutputfile 是文件的以 XML 格式，控制台输出写入到的名称。|  
|5|-l/log|否|logfile|有效的文件名。|  
|6|-e/projectenvironment|否|projectenvironmentfolder|有效的文件夹名称包含 SSMA 项目环境文件。|  
|7|-p/securepassword|否|-a/add {<server_id> [,...n] &#124; all} -c&#124;serverconnection  <server-connection-file> [-v&#124;variable <variable-value-file>] [-o/overwrite]<br /><br />或<br /><br />-a/add {<server_id> [,...n] &#124; all} -s&#124;script <script-file> [-v&#124;variable <variable-value-file>] [-o/overwrite]<br /><br />-r/remove {<server_id> [, ...n] &#124; all}<br /><br />-l/list<br /><br />-e/export {<server-id> [, ...n] &#124; all} <encrypted-password -file><br /><br />-i/import {<server-id> [, ...n] &#124; all} <encrypted-password-file>|如果指定，此选项不能结合任何其他选项配合使用。<br /><br />服务器 id:为 {string} 的服务器提供唯一 ID<br /><br />服务器连接文件： 服务器定义文件 （serverconnectionfile 或脚本文件）。<br /><br />变量值文件：它是一个变量定义文件，并使用服务器连接文件中。<br /><br />加密密码的文件：它是使用用户指定通行短语加密的服务器的密码文件。|  
|8|-?|否|不适用|不适用|  
  
## <a name="see-also"></a>请参阅  
[执行 SSMA 控制台 (Oracle)](https://msdn.microsoft.com/7228ccba-c69f-4b4c-8664-01a2750183c5)  
  
