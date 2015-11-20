###M3: Save UI Element as Image

本小节将介绍如何将页面元素保存为图片，在前一小节中，我们加入了名称为gridMsg的`Grid Control`，现在我们将使用`RenderTargetBitmap`把gridMsg这个页面元素保存为一张图片。在将gridMsg保存为图片时，会将gridMsg的子元素包括Border和TextBlock一并存储为图片的一部分。学习完本节内容，您能够通过`RenderTargetBitmap`将任何的页面元素存储成图片。

+ 定义Button1(btnSendMail)的单击事件  
+ 在单击事件方法中，将gridMsg及其子元素存储成图片

打开Card程序， 在`MainPage.xaml`中，定位到btnSendMail控件，新添加单击事件`SendMail_Click`，修改后代码如下：

	<Button x:Name="btnSendMail" Content="Send to Friend" Grid.Row="1" Margin="4" Click="SendMail_Click"/>

然后，用鼠标在`SendMail_Click`中任何位置单击， 在键盘上按下F12键，进入`Code Behind`代码。

在`MainPage.xaml.cs`文件中，使用关键字`async`将SendMail_Click方法修改为异步方法。

	private async void SendMail_Click(object sender, RoutedEventArgs e)
    {
	}

在页面顶部，添加命名空间引用：

	using Windows.Graphics.Imaging;
	using Windows.Storage;

返回`SendMail_Click`方法中，实现程序逻辑如下：

    private async void SendMail_Click(object sender, RoutedEventArgs e)
    {
        RenderTargetBitmap renderTrgBitmap = new RenderTargetBitmap();
        await renderTrgBitmap.RenderAsync(gridMsg);

        var pixelBuffer = await renderTrgBitmap.GetPixelsAsync();
        var file = await KnownFolders.PicturesLibrary.CreateFileAsync("Wishes.jpg", CreationCollisionOption.ReplaceExisting);

        using (var stream = await file.OpenAsync(FileAccessMode.ReadWrite))
        {
            var encoder = await BitmapEncoder.CreateAsync(BitmapEncoder.JpegEncoderId, stream);
            encoder.SetPixelData(BitmapPixelFormat.Bgra8,
                BitmapAlphaMode.Straight,
                (uint)renderTrgBitmap.PixelWidth,
                (uint)renderTrgBitmap.PixelHeight,
                96d, 96d,
                pixelBuffer.ToArray());

            await encoder.FlushAsync();
        }
    }

在以上代码中，首先使用`RenderTargetBitmap`（在`Windows.UI.Xaml.Media.Imaging`中）将gridMsg`Grid Control`转化为内存对象，然后使用`BitmapEncoder`（在`Windows.Graphics.Imaging`中）将内存对象写入到**Picture Library**中Wishes.jpg文件中。

####修改Capabilities声明  
在Solution Explorer中， 双击打开`Package.appxmanifest`文件。单击Capabilities选项卡，在Capabilities列表中，勾选**Picture Library**

运行程序，单击**Send to Friend**, 然后切换到**Pictures**文件夹，查看生成的Wishes.jpg。
