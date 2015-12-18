<properties
	pageTitle="捕获 Windows VM 的镜像| Windows Azure"
	description="捕获使用经典部署模型创建的 Windows 虚拟机的镜像。"
	services="virtual-machines"
	documentationCenter=""
	authors="cynthn"
	manager="timlt"
	editor="tysonn"
	tags="azure-service-management"/>

<tags
	ms.service="virtual-machines"
	ms.date="07/16/2015"
        wacn.date="11/12/2015"/>

#捕获使用经典部署模型创建的 Windows 虚拟机的镜像。

[AZURE.INCLUDE [了解部署模型](../includes/learn-about-deployment-models-include.md)]本文介绍如何使用经典部署模型创建资源。

本文将演示如何捕获运行 Windows 的 Azure 虚拟机，你可以将它用作镜像来创建其他虚拟机。此镜像包含操作系统磁盘和任何附加到虚拟机的数据磁盘。由于它不包括网络配置，因此你在使用此模板创建其他虚拟机时，需要进行相关配置。

Azure 将镜像存储在**“我的镜像”**下。你上载的任何镜像都会存储在同一位置。有关镜像的详细信息，请参阅关于 [Azure 中的虚拟机镜像] []。

##开始之前##

这些步骤假定你已创建了 Azure 虚拟机并配置了操作系统，包括附加任何数据磁盘。如果你尚未执行此操作，请参阅以下说明：

- [创建运行 Windows 的自定义虚拟机][]
- [如何将数据磁盘附加到虚拟机][]

> [AZURE.WARNING]此过程将在捕获原始虚拟机后将该虚拟机删除，它不应作为备份虚拟机的方法。执行此操作的一个可行方法是 Azure 备份，它在特定区域中作为预览版提供。有关详细信息，请参阅[备份 Azure 虚拟机](/documentation/articles/backup/backup-azure-vms)。认证合作伙伴提供了其他解决方案。若要了解当前提供的内容，请搜索 Azure 应用商店。

##捕获虚拟机##

1. 在 [Azure 门户](http://manage.windowsazure.cn)中，**连接**到虚拟机。有关说明，请参阅[如何登录到运行 Windows Server 的虚拟机][]。

2.	以管理员身份打开“命令提示符”窗口。

3.	将目录更改为 `%windir%\system32\sysprep`，然后运行 sysprep.exe。

4. 	此时会显示**“系统准备工具”**对话框。请执行以下操作：

	- 在**“系统清理操作”**中，选择**“进入系统全新体验(OOBE)”**，并确保选中**“一般化”**。有关使用 Sysprep 的详细信息，请参阅[如何使用 Sysprep：简介][]。

	- 在**“关机选项”**中选择**“关机”**。

	- 单击**“确定”**。

	![运行 Sysprep](./media/virtual-machines-capture-image-windows-server/SysprepGeneral.png)

7.	Sysprep 将关闭虚拟机，这会在 Azure 门户中将虚拟机的状态更改为**“已停止”**。

8.	在 Azure 门户中，单击**“虚拟机”**，然后选择要捕获的虚拟机。

9.	在命令栏中，单击**“捕获”**。

	![捕获虚拟机](./media/virtual-machines-capture-image-windows-server/CaptureVM.png)

	此时将显示**“捕获虚拟机”**对话框。

10.	在**“镜像名称”**中，键入新镜像的名称。

11.	在将 Windows Server 镜像添加到自定义镜像组之前，必须先按前面步骤中的说明通过运行 Sysprep 将该镜像通用化。单击**“我已经在虚拟机上运行了 Sysprep”**以指明你已完成此操作。

12.	单击复选标记以捕获镜像。新镜像现在将显示在**“镜像”**下。

 	![成功捕获镜像](./media/virtual-machines-capture-image-windows-server/VMCapturedImageAvailable.png)

##后续步骤##
该镜像已就绪，可用于创建虚拟机了。为此，你将通过使用**“从库中”**菜单项并选择你刚创建的镜像来创建一个虚拟机。有关说明，请参阅[创建运行 Windows 的自定义虚拟机][]。

[创建运行 Windows 的自定义虚拟机]: /documentation/articles/virtual-machines-windows-create-custom
[如何将数据磁盘附加到虚拟机]: /documentation/articles/storage-windows-attach-disk
[如何登录到运行 Windows Server 的虚拟机]: /documentation/articles/virtual-machines-log-on-windows-server
[如何使用 Sysprep：简介]: http://technet.microsoft.com/zh-cn/library/bb457073.aspx
[Run Sysprep.exe]: ./media/virtual-machines-capture-image-windows-server/SysprepCommand.png
[Enter Sysprep.exe options]: ./media/virtual-machines-capture-image-windows-server/SysprepGeneral.png
[The virtual machine is stopped]: ./media/virtual-machines-capture-image-windows-server/SysprepStopped.png
[Capture an image of the virtual machine]: ./media/virtual-machines-capture-image-windows-server/CaptureVM.png
[Enter the image name]: ./media/virtual-machines-capture-image-windows-server/Capture.png
[Image capture successful]: ./media/virtual-machines-capture-image-windows-server/CaptureSuccess.png
[Use the captured image]: ./media/virtual-machines-capture-image-windows-server/MyImagesWindows.png

<!---HONumber=79-->