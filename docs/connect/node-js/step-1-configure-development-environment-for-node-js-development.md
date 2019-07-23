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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68003757"
---
# <a name="step-1--configure-development-environment-for-nodejs-development"></a>步骤 1：配置用于 Node.js 开发的开发环境
需要使用必备组件配置开发环境, 以便使用 node.js 驱动程序为 SQL Server 开发应用程序。  最常见的方法是使用节点包管理器 (npm) 来安装单调乏味的模块, 但你可以根据需要直接在[Github](https://github.com/pekim/tedious)上下载枯燥的模块。  
  
请注意, node.js 驱动程序使用 TDS 协议, 该协议默认情况下在 SQL Server 和 Azure SQL 数据库中启用。  这种方式无需任何其他配置。  
  
## <a name="windows"></a>Windows  
  
1. **安装 node.js 运行时和 npm 包管理器**  
A. 中转到[node.js](https://nodejs.org/en/download/)  
B. 单击相应的 "Windows installer msi" 链接。   
c. 下载后, 运行 msi 以安装 node.js  
  
2. **打开 cmd.exe**  
  
3. **创建一个项目目录**, 然后导航到该目录。    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
4. **创建节点项目。**  若要在项目创建期间保留默认值, 请在创建项目之前按 enter。 在此步骤结束时, 你应在项目目录中看到一个 package 文件。  
```  
> npm init  
```  
  
5. **在项目中安装繁琐的模块。**  这是驱动程序用来与 SQL Server 通信的 TDS 协议的实现。  
```  
> npm install tedious  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1.  **打开终端**  
  
2. **安装 node.js 运行时**  
```  
>sudo apt-get install node  
```  
3. **安装 npm (node 包管理器)**  
```  
> sudo apt-get install npm  
```  
4. **创建一个项目目录**, 然后导航到该目录。    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
5. **创建节点项目。**  若要在项目创建期间保留默认值, 请在创建项目之前按 enter。 在此步骤结束时, 你应在项目目录中看到一个 package 文件。  
```  
> sudo npm init  
```  
  
6. **在项目中安装繁琐的模块。**  这是驱动程序用来与 SQL Server 通信的 TDS 协议的实现。  
```  
> sudo npm install tedious  
```  
  
## <a name="mac"></a>Mac  
  
1. **安装 node.js 运行时和 npm 包管理器**  
A. 中转到[node.js](https://nodejs.org/en/download/)  
B. 单击相应的 Mac OS 安装程序 "链接。  
c. 下载完成后, 运行 dmg 以安装 node.js  
  
2. **打开终端**  
  
3. **创建一个项目目录**, 然后导航到该目录。    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
4. **创建节点项目。**  若要在项目创建期间保留默认值, 请在创建项目之前按 enter。 在此步骤结束时, 你应在项目目录中看到一个 package 文件。  
```  
> npm init  
```  
  
5. **在项目中安装繁琐的模块。**  这是驱动程序用来与 SQL Server 通信的 TDS 协议的实现。  
```  
> npm install tedious  
```  
  
