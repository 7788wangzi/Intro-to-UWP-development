###M4: Use CommandBar
本小节将介绍如何使用`CommandBar`, CommandBar分为`PrimaryCommands`和`SecondaryCommands`，在`PrimaryCommands`中不要放置多于四个按钮。然后将不常使用的命令放到`SecondaryCommands`中。 

在`MainPage.xaml`页面， 添加`Page.BottomAppBar`， 在CommandBar中新添加四个`AppBarButton`。在CommandBar.SecondaryCommands中添加一个`Menu Item`。

打开Card程序， 在`MainPage.xaml`页面， 在`</Page>`之前，新添加`Page.BottomAppBar`控件。  
在Page.BottomAppBar控件中， 新添加`CommandBar`控件， 修改后代码如下：
    
	<Page.BottomAppBar>
        <CommandBar>
        </CommandBar>
    </Page.BottomAppBar>

	</Page>
在CommandBar中加入第一个`AppBarButton Control`， 命名为abtnGetWishes， 设置其`Icon`属性，`Label`属性。

	<AppBarButton x:Name="abtnGetWishes" Icon="Play" Label="Wishes" />

同样加入其它三个`AppBarButton Control`， 并设置相应属性。

    <AppBarButton x:Name="abtnGetWishes" Icon="Play" Label="Wishes" />
    <AppBarButton x:Name="abtnSendFriend" Icon="Send" Label="Wishes" />
    <AppBarButton x:Name="abtnOpenFile" Icon="Pictures" Label="Wishes" />
    <AppBarButton x:Name="abtnOpenCamera" Icon="Camera" Label="Wishes" />

加入二级菜单项目。

    <CommandBar.SecondaryCommands>
        <AppBarButton x:Name="abtnLike" Icon="Like" Label="Like" />
    </CommandBar.SecondaryCommands>

在第二和第三个AppBarButton之间加入`AppBarSeparator`，将命令分组。

	<AppBarSeparator />

然后，定义abtnGetWishes的单击事件为`GetMessage_Click`， 定义abtnSendFriend的单击事件为`SendMail_Click`。

修改后代码如下：

    <Page.BottomAppBar>
        <CommandBar>
            <AppBarButton x:Name="abtnGetWishes" Icon="Play" Label="Wishes" Click="GetMessage_Click"/>
            <AppBarButton x:Name="abtnSendFriend" Icon="Send" Label="Send" Click="SendMail_Click"/>
            <AppBarSeparator />
            <AppBarButton x:Name="abtnOpenFile" Icon="Pictures" Label="Open" />
            <AppBarButton x:Name="abtnOpenCamera" Icon="Camera" Label="Camera" />
            <CommandBar.SecondaryCommands>
                <AppBarButton x:Name="abtnLike" Icon="Like" Label="Like" />
            </CommandBar.SecondaryCommands>
        </CommandBar>
    </Page.BottomAppBar>

运行程序， 查看新添加CommandBar效果。