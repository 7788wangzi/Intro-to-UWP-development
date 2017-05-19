# Exercise 3：XAML Controls(2)

在前小节中，我们在Card程序的主界面中加入了简单的XAML控件， 本小节将在其基础上进行优化，使界面看上去更加美观。本小节用到了`Grid Control`, `Border Control`，以及XAML控件的`VerticalAlignment`，`HorizontalAlignment`， `Padding`， `Margin`， `TextWrapping`等属性。

打开Card程序，右键单击**Assets**文件夹，选择**Add**， **Existing Item...**， 选择一张JPG图片（我们这里的图片名称为background.jpg)，这张图片将用作贺卡的背景。单击Add按钮。
切换到`MainPage.xaml`页面，定位到StackPanel控件， 为StackPanel添加`Padding`属性。 分别为Button1和Button2添加`Margin`属性，修改后代码如下：

    <StackPanel Orientation="Horizontal" Grid.Row="1" Padding="4">
        <Button x:Name="btnSendMail" Content="Send to Friend" Grid.Row="1" Margin="4"/>
        <Button x:Name="btnGetMessage" Content="Get a Wishes" Grid.Row="1" Click="GetMessage_Click" Margin="4"/>
    </StackPanel>

定位到`TextBlock Control`，新添加`FontSize`属性和``，并设置水平居中对齐。 

	<TextBlock x:Name="tbMessage" Text="Hello, Click to Start..." Grid.Row="0" FontSize="34" HorizontalAlignment="Center"  TextWrapping="Wrap"/>

在页面上新添加一个`Border Control`，将TextBlock包裹。并设置Border的透明度属性`Opacity`, 背景属性`Background`, 垂直对齐属性`VerticalAlignment`， 修改后代码如下：

    <Border Opacity="0.8" Background="White" VerticalAlignment="Center">
        <TextBlock x:Name="tbMessage" Text="Hello, Click to Start..." Grid.Row="0" FontSize="34" HorizontalAlignment="Center"  TextWrapping="Wrap"/>
    </Border>

在页面上新添加一个`Grid Control`, 将其放在Grid第一行，Grid用于显示贺卡的背景。

    <Grid x:Name="gridMsg" Grid.Row="0" >            
        <Border Opacity="0.8" Background="White" VerticalAlignment="Center">
            <TextBlock x:Name="tbMessage" Text="Hello, Click to Start..." Grid.Row="0" FontSize="34" HorizontalAlignment="Center"  TextWrapping="Wrap"/>
        </Border>
    </Grid>

再返回到`MainPage.xaml.cs`页面， 在构造方法中加入`Loaded`事件， 在Loaded方法中，我们为gridMsg设置背景图片。

    public MainPage()
    {
        this.InitializeComponent();
        this.Loaded += MainPage_Loaded;
    }

    private void MainPage_Loaded(object sender, RoutedEventArgs e)
    {
        ImageBrush imageBrush = new ImageBrush();
        imageBrush.ImageSource = new BitmapImage(new Uri(@"ms-appx:///Assets/background.jpg"));
        imageBrush.Stretch = Stretch.UniformToFill;
        gridMsg.Background = imageBrush;
    }

其中，使用BitmapImage前要引入命名空间`using Windows.UI.Xaml.Media.Imaging;`。
