### M5: Use File Storage
本小节介绍UWP中的文件操作，使用到了`FileOpenPicker`API(在`Windows.Storage.Pickers`中）。本例中，单击**打开**文件按钮，然后在图片库中选择照片，将选择的照片用作贺卡背景。学完本节课程，您能够使用`FileOpenPicker`来打开设备文件。留个小作业，请探索使用`FileSavePicker`将文件保存到设备。

在`MainPage.xaml`页面，定位到abtnOpenFile控件，定义单击事件为`OpenFile_Click`。

	<AppBarButton x:Name="abtnOpenFile" Icon="Pictures" Label="Open" Click="OpenFile_Click"/>

然后，用鼠标在`OpenFile_Click`中任何位置单击， 在键盘上按下F12键，进入`Code Behind`代码。

使用关键字`async`将OpenFile_Click修改为异步方法。

    private async void OpenFile_Click(object sender, RoutedEventArgs e)
    {
    }

定义`FileOpenPicker`对象， 将文件浏览位置设置为`PickerLocationId.PicturesLibrary`， 将浏览文件类型设置为.jpg和.png，代码如下：

    FileOpenPicker fileOpenPicker = new FileOpenPicker();
    fileOpenPicker.SuggestedStartLocation = PickerLocationId.PicturesLibrary;
    fileOpenPicker.FileTypeFilter.Add(".jpg");
    fileOpenPicker.FileTypeFilter.Add(".png");

    StorageFile photo = await fileOpenPicker.PickSingleFileAsync();

然后，通过文件流方式将StorageFile传给BitmapImage，再将BitmapImage传给ImageBrush，进而设置为gridMsg的背景。

    if (photo == null)
        return;

    BitmapImage bitmapImage = new BitmapImage();
    using (IRandomAccessStream stream =await photo.OpenAsync(FileAccessMode.Read))
    {
        bitmapImage.SetSource(stream);
    }

    ImageBrush imageBrush = new ImageBrush();
    imageBrush.ImageSource = bitmapImage;
    gridMsg.Background = imageBrush;

其中， IRandomAccessStream来自于`Windows.Storage.Streams`，用于以流的形式访问文件。

