# Exercise 8: Use Camera

本小节介绍UWP中摄像头的使用，使用`CameraCaptureUI`来拍照，不仅能够获得图像，还能够对图像进行剪裁 (目前Mobile设备还上不支持)。 在本例中， 单击Camera按钮调用摄像头来拍摄图像， 并使用`CameraCaptureUI.PhotoSettings.CroppedSizeInPixels`对图像进行剪裁。

在`MainPage.xaml`页面，定位到abtnOpenCamera控件，定义单击事件为`Camera_Click`。

	<AppBarButton x:Name="abtnOpenCamera" Icon="Camera" Label="Camera" Click="Camera_Click"/>

然后，用鼠标在`Camera_Click`中任何位置单击，在键盘上按下F12键，进入`Code Behind`代码。

使用关键字`async`将Camera_Click修改为异步方法。

    private async void Camera_Click(object sender, RoutedEventArgs e)
    {
    }

定义`CameraCaptureUI`对象，设置图像格式为`CameraCaptureUIPhotoFormat.Jpeg`，设置剪裁大小为400X400，代码如下：

    var cameraCaptureUI = new CameraCaptureUI();
    cameraCaptureUI.PhotoSettings.Format = CameraCaptureUIPhotoFormat.Jpeg;
    cameraCaptureUI.PhotoSettings.AllowCropping = true;
    cameraCaptureUI.PhotoSettings.CroppedSizeInPixels = new Size(400, 400);

    StorageFile photo = await cameraCaptureUI.CaptureFileAsync(CameraCaptureUIMode.Photo);

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
