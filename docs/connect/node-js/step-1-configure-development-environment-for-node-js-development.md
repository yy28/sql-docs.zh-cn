---
title: 步骤 1：配置用于 Node.js 开发的开发环境 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 2dad01f1-fadf-4ac9-9b4d-26be3d301886
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bce89cc12c7493522de55adffb69fcbe3307cbdf
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "68003757"
---
# <a name="step-1--configure-development-environment-for-nodejs-development"></a>步骤 1：配置用于 Node.js 开发的开发环境
必须为开发环境配置必备项，才能使用 Node.js Driver for SQL Server 开发应用程序。  最常见的方法是，使用节点包管理器 (npm) 安装 tedious 模块，但如果你愿意，也可以直接从 [Github](https://github.com/pekim/tedious) 下载 tedious 模块。  
  
请注意，Node.js 驱动程序使用 TDS 协议，SQL Server 和 Azure SQL 数据库中默认启用此协议。  这种方式无需任何其他配置。  
  
## <a name="windows"></a>Windows  
  
1. **安装 Node.js 运行时和 npm 包管理器**  
a. 转到 [Node.js](https://nodejs.org/en/download/)  
b. 单击相应的 Windows 安装程序 msi 链接。   
c. 下载后，运行 msi 来安装 Node.js  
  
2. **打开 cmd.exe**  
  
3. 创建项目目录  ，然后转到此目录。    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
4. **创建 Node 项目。**  若要在项目创建期间保留默认设置，请一直按 Enter 键，直到项目创建为止。 在这一步结束时，应该会在项目目录中看到一个 package.json 文件。  
```  
> npm init  
```  
  
5. **在项目中安装 tedious 模块。**  这是驱动程序用来与 SQL Server 通信的 TDS 协议的实现。  
```  
> npm install tedious  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1.  **打开终端**  
  
2. **安装 Node.js 运行时**  
```  
>sudo apt-get install node  
```  
3. **安装 npm（节点包管理器）**  
```  
> sudo apt-get install npm  
```  
4. 创建项目目录  ，然后转到此目录。    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
5. **创建 Node 项目。**  若要在项目创建期间保留默认设置，请一直按 Enter 键，直到项目创建为止。 在这一步结束时，应该会在项目目录中看到一个 package.json 文件。  
```  
> sudo npm init  
```  
  
6. **在项目中安装 tedious 模块。**  这是驱动程序用来与 SQL Server 通信的 TDS 协议的实现。  
```  
> sudo npm install tedious  
```  
  
## <a name="mac"></a>Mac  
  
1. **安装 Node.js 运行时和 npm 包管理器**  
a. 转到 [Node.js](https://nodejs.org/en/download/)  
b. 单击相应的 Mac OS 安装程序链接。  
c. 下载后，运行 dmg 来安装 Node.js  
  
2. **打开终端**  
  
3. 创建项目目录  ，然后转到此目录。    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
4. **创建 Node 项目。**  若要在项目创建期间保留默认设置，请一直按 Enter 键，直到项目创建为止。 在这一步结束时，应该会在项目目录中看到一个 package.json 文件。  
```  
> npm init  
```  
  
5. **在项目中安装 tedious 模块。**  这是驱动程序用来与 SQL Server 通信的 TDS 协议的实现。  
```  
> npm install tedious  
```  
  
