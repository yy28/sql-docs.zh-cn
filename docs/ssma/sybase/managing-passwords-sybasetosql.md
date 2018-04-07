---
title: 管理密码 (SybaseToSQL) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Sybase Console,Exporting or Importing Encrypted Passwords
- Sybase Console,Managing Passwords
- Sybase Console,Securing Password
ms.assetid: 9b6a70f9-6840-4140-a059-bb7bd7ccc67c
caps.latest.revision: 12
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6c46c70586697101f8e1e1f22f3506e1978bb70f
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="managing-passwords-sybasetosql"></a>管理密码 (SybaseToSQL)
本节是有关保护数据库密码和导入或将其导出跨服务器的过程：  
  
1.  保护密码  
  
2.  导出或导入加密的密码  
  
## <a name="securing-password"></a>保护密码  
SSMA 允许你保护你的数据库的密码。  
  
使用以下过程来实现安全的连接：  
  
指定一个有效的密码，使用以下三种方法之一：  
  
1.  **明文形式：** 'password' 节点的值属性中键入数据库密码。 它是在脚本文件或服务器连接文件的服务器部分中的服务器定义节点下找到。  
  
    以明文形式的密码是不安全的。 因此，你将遇到控制台输出中的以下警告消息： *"服务器&lt;服务器 id&gt;密码是提供以不安全的明文形式，SSMA 控制台应用程序提供了一个选项来保护密码通过加密，请参阅帮助文件了解详细信息中 SSMA – securepassword 选项。"*  
  
    **加密的密码：**指定的密码，在这种情况下，存储在 ProtectedStorage.ssma 的本地计算机上以加密形式。  
  
    -   **保护密码**  
  
        -   执行`SSMAforSybaseConsole.exe`与`–securepassword`并在命令行传递包含中的服务器定义部分的密码节点的连接或脚本文件的服务器添加交换机。  
  
        -   在提示符下，要求用户输入数据库密码并确认它。  
  
            服务器定义 id 和其相应的加密的密码存储在本地计算机上的文件  
            
            示例 1：  
            
                Specify password
                
                C:\SSMA\SSMAforSybaseConsole.EXE –securepassword –add all –s "D:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\AssessmentReportGenerationSample.xml" –v "D:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ VariableValueFileSample.xml"
                
                Enter password for server_id 'XXX_1': xxxxxxx
                
                Re-enter password for server_id 'XXX_1': xxxxxxx
            
            示例 2：
            
                C:\SSMA\SSMAforSybaseConsole.EXE –securepassword –add "source_1,target_1" –c "D:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ServersConnectionFileSample.xml" – v "D:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ VariableValueFileSample.xml" -o
                
                Enter password for server_id 'source_1': xxxxxxx
                
                Re-enter password for server_id 'source_1': xxxxxxx
                
                Enter password for server_id 'target_1': xxxxxxx
                
                Re-enter password for server_id 'target _1': xxxxxxx  
    
    -   **删除加密的密码**  
  
        执行`SSMAforSybaseConsole.exe`与`–securepassword`和`–remove`切换在将服务器 id，以从本地计算机上存在的受保护的存储文件中删除加密的密码传递的命令行。  
  
        例如：  
        
            C:\SSMA\SSMAforSybaseConsole.EXE –securepassword –remove all
            C:\SSMA\SSMAforSybaseConsole.EXE –securepassword –remove "source_1,target_1"  
  
    -   **列出其密码进行加密的服务器 Id**  
  
        执行`SSMAforSybaseConsole.exe`与`–securepassword`和`–list`切换在命令行，若要列出其密码已加密的所有服务器 id。  
  
        例如：  
        
            C:\SSMA\SSMAforSybaseConsole.EXE –securepassword –list  
  
    > [!NOTE]  
    > 1.  在脚本或服务器的连接文件中提到的明文密码将优先于受保护的文件中的加密密码。  
    > 2.  服务器连接文件或脚本文件的服务器部分中不存在的任何密码时或者如果它不在固定在本地计算机上，则控制台将提示您输入的密码。  
  
## <a name="exporting-or-importing-encrypted-passwords"></a>导出或导入加密的密码  
SSMA 控制台应用程序，可将加密的数据库密码存在于本地计算机上的文件导出到受保护的文件，反之亦然。 该步骤有助于使加密的密码机独立。 导出功能读取服务器 id 和密码从本地受保护的存储，并将信息保存在一个加密文件。 系统会提示用户输入的受保护的文件的密码。 请确保输入的密码为 8 个字符长度或更大。 在不同计算机之间，此受保护的文件是可移植的。 导入功能从受保护的文件读取服务器 id 和密码信息。 用户提示您输入的受保护的文件的密码，并将信息追加到受保护的本地存储。  
  
例如：  

    Export password
    
    Enter password for protecting the exported file
    
    C:\SSMA\SSMAforSybaseConsole.EXE –securepassword –export all "machine1passwords.file"
    
    Enter password for protecting the exported file: xxxxxxxx
    
    Please confirm password: xxxxxxxx
    
    C:\SSMA\SSMAforSybaseConsole.EXE –p –e "SybaseDB_1_1,Sql_1" "machine2passwords.file"
    
    Enter password for protecting the exported file: xxxxxxxx
    
    Please confirm password: xxxxxxxx  
  
例如：  

    Import an encrypted password
    
    Enter password for protecting the imported file
    
    C:\SSMA\SSMAforSybaseConsole.EXE –securepassword –import all "machine1passwords.file"
    
    Enter password to import the servers from encrypted file: xxxxxxxx
    
    Please confirm password: xxxxxxxx
    
    C:\SSMA\SSMAforSybaseConsole.EXE –p –i "SybaseDB_1,Sql_1" "machine2passwords.file"
    
    Enter password to import the servers from encrypted file: xxxxxxxx
    
    Please confirm password: xxxxxxxx  
  
## <a name="see-also"></a>另请参阅  
[执行 SSMA 控制台 (Sybase)](http://msdn.microsoft.com/en-us/ea8950b7-fabc-4aa4-89f8-9573a2617d70)  
  
