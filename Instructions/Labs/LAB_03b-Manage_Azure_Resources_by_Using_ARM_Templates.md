﻿---
lab:
    title: '03b - 使用 ARM 模板管理 Azure 资源'
    module: '模块 03 - Azure 管理'
---

# 实验室 03b - 使用 ARM 模板管理 Azure 资源
# 学生实验室手册

## 实验室场景
你已经探索了与通过使用 Azure 门户基于资源组对资源进行预配和组织相关的基本 Azure 管理功能，现在需要使用 Azure 资源管理器模板执行同等的任务。

## 目标

在本实验室中，你将：

+ 任务 1：查看用于部署 Azure 托管磁盘的 ARM 模板
+ 任务 2：通过使用 ARM 模板创建 Azure 托管磁盘
+ 任务 3：查看基于 ARM 模板的托管磁盘部署

## 预计用时：20 分钟

## 说明

### 练习 1：

#### 任务 1：查看用于部署 Azure 托管磁盘的 ARM 模板

在本任务中，你将使用一个 Azure 资源管理器模板创建一个新的 Azure 磁盘资源。

1. 登录到 [Azure 门户](https://portal.azure.com)。

1. 在 Azure 门户中，搜索并选择 **“资源组”**。 

1. 在资源组列表中，单击 **“az104-03a-rg1”**。

1. 在 **“az104-03a-rg1”** 资源组边栏选项卡中的 **“设置”** 部分，单击 **“部署”**。

1. 在 **“az104-03a-rg1 - 部署”** 边栏选项卡上，单击部署列表中的第一项，然后单击 **“查看模板”**。

    >**说明**：查看模板内容，请注意，你可以选择将其下载到本地计算机，并添加到库中，然后重新部署。

1. 单击 **“下载”** 并将包含模板和参数文件的压缩文件保存到实验室计算机上的 **“下载”** 文件夹。

1. 将下载文件的内容提取到实验室计算机上的 **下载** 文件夹。

    >**说明**：这些文件也可以通过以下途径提供 **\\Allfiles\\Labs\\03\\az104-03b-md-template.json** 和 **\\Allfiles\\Labs\\03\\az104-03b-md-parameters.json**

#### 任务 2：通过使用 ARM 模板创建 Azure 托管磁盘

1. 在 Azure 门户中，搜索并选择 **“模板部署(使用自定义模板进行部署)”**。

1. 在 **“自定义部署”** 边栏选项卡上，单击 **“在编辑器中构建自己的模板”**。

1. 在 **“编辑模版”** 边栏选项卡上，单击 **“加载文件”** 并上传你在上一步中下载的模板文件。

1. 在编辑器窗格中，移除以下行：

   ```json
   "sourceResourceId": {
       "type": "String"
   },
   "sourceUri": {
       "type": "String"
   },
   "osType": {
       "type": "String"
   },
   ```

   ```json
   },
   "hyperVGeneration": {
       "defaultValue": "V1",
       "type": "String"
   ```

   ```json
   "osType": "[parameters('osType')]"
   ```

    >**注意**：由于这些参数不适用于当前部署，因此将其移除。sourceResourceId、sourceUri、osType 和 hyperVGeneration 参数尤其适用于从现有的 VHD 文件中创建 Azure 磁盘。

1. 此外，从以下行中删除尾随逗号：

   ```json
   "diskSizeGB": "[parameters('diskSizeGb')]",
   ```

    >**注意**：需要对基于 JSON 的 ARM 模板的语法规则作出解释。

1. 保存更改。

1. 返回到 **“自定义部署”** 边栏选项卡，单击 **“编辑参数”**。 

1. 在 **“编辑参数”** 的边栏选项卡上，单击 **“加载文件”** 并上传参数文件 **“\\Allfiles\\Labs\\03\\az104-03b-md-parameters.json”**，然后保存更改。

1. 返回 **“自定义部署”** 边栏选项卡，指定以下设置：

    | 设置 | 数值 |
    | --- |--- |
    | 订阅 | 你在本实验室中使用的 Azure 订阅的名称 |
    | 资源组 | 新资源组的名称 **az104-03b-rg1** |
    | 位置 | 此实验室中正在使用的订阅中可用的任何 Azure 区域的名称 |
    | 磁盘名称 | **az104-03b-disk1** |
    | 位置 | 接受默认值 |
    | SKU | **Standard_LRS** |
    | 磁盘大小 (Gb) | **32** |
    | 创建选项 | **空** |

1. 勾选 **“我同意上述条款和条件”** 复选框 ，然后单击 **“购买”**。

1. 验证部署是否成功完成。

#### 任务 3：查看基于 ARM 模板的托管磁盘部署

1. 在 Azure 门户中，搜索并选择 **“资源组”**。 

1. 在资源组列表中，单击 **“az104-03b-rg1”**。

1. 在 **“az104-03b-rg1”** 资源组边栏选项卡中的 **“设置”** 部分，单击 **“部署”**。

1. 在 **“az104-03b-rg1 - 部署”** 边栏选项卡上，单击部署列表中的第一个条目，然后查看 **“输入”** 和 **“模板”** 边栏选项卡的内容。

#### 清理资源

   >**说明**：不要删除你在本实验室中部署的资源。在本模块的下一个实验室中，你将引用它们。

#### 回顾

在本实验室中，你已：

- 查看了用于部署一个 Azure 托管磁盘的 ARM 模板
- 使用 ARM 模板创建一个 Azure 托管磁盘
- 查看了基于 ARM 模板的托管磁盘部署
