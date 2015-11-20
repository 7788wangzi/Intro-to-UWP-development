###M2：XAML Controls

本小节介绍如何在界面上添加简单的XAML Controls, 本例中我们用到了`Grid`， `TextBlock`， `Button`， 和`StackPanel`控件。XAML自身所有的控件都声明在`Windows.UI.Xaml.Controls`这个类库中， 您可以去MSDN[1]详细了解各种XAML控件的使用。

我们要实现一个感恩节贺卡程序，其界面由一个文本显示控件`TextBlock`，和两个按钮控件`Button`组成。 Button1用于获取一个贺卡的祝福语，Button2用于将当前的祝福语通过邮件发送给朋友。

请确保您已经完成了前一章节的内容。

在`Grid Control`中添加2个**行**声明。

    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <Grid.RowDefinitions>
            <RowDefinition Height="*"/>
            <RowDefinition Height="Auto"/>
        </Grid.RowDefinitions>

    </Grid>

在页面上，新添加一个`TextBlock Control`， 并将其位置定位在Grid的第一行。设置其属性如下:

	<TextBlock x:Name="tbMessage" Text="Hello, Click to Start..." Grid.Row="0"/>

在页面上， 新添加两个`Button Control`，并将其位置定位在Grid的第二行。设置其属性如下：

	<Button x:Name="btnSendMail" Content="Send to Friend" Grid.Row="1" />
	<Button x:Name="btnGetMessage" Content="Get a Wishes" Grid.Row="1" />

现在切换到可视化界面， 我们发现步骤2中添加到两个Button是重合在一起的，为了使得两个Button能够并排，我们添加第三个控件`StackPanel Control`， 并使用StackPanel将两个Button包裹。修改后我们的代码如下：

    <StackPanel Orientation="Horizontal" Grid.Row="1" Padding="4">
        <Button x:Name="btnSendMail" Content="Send to Friend" Grid.Row="1"/>
        <Button x:Name="btnGetMessage" Content="Get a Wishes" Grid.Row="1"/>
    </StackPanel>

首先，让我们实现获取祝福语的程序逻辑。在tbGetMessage Button的属性中，添加单击事件`GetMessage_Click`， 修改后的代码如下：

	<Button x:Name="btnGetMessage" Content="Get a Wishes" Grid.Row="1" Click="GetMessage_Click"/>

然后，用鼠标在`GetMessage_Click`中任何位置单击， 在键盘上按下F12键，进入`Code Behind`代码。
在`MainPage.xaml.cs`文件中，在`GetMessage_Click`方法中，实现程序逻辑如下：

+	定义字符串变量str。  
+	将str的值赋值给`TextBlock`的Text属性。	  

代码如下：

    private void GetMessage_Click(object sender, RoutedEventArgs e)
    {
        string str = "Happy Thanksgiving!";
        tbMessage.Text = str;
    }


[1]: https://msdn.microsoft.com/en-us/library/windows/apps/xaml/jj203560.aspx