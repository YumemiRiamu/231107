# 231107 비주얼프로그래밍 과제 

20191276 컴퓨터공학과 양용석</br>


WinUI3 에서 Win2D를 활용하여 5가지 이상의 도형이나 글씨를 구현</br>


코드</br>

```
//MainWindow.xaml
<Window
    x:Class="App4.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:App4"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    xmlns:canvas="using:Microsoft.Graphics.Canvas.UI.Xaml"
    mc:Ignorable="d">
    <Grid>
        <canvas:CanvasControl
            PointerMoved="CanvasControl_PointerMoved" Draw="CanvasControl_Draw" ClearColor="CornflowerBlue"/>
    </Grid>
</Window>

```

```
//MainWindow.xaml.h
#include "MainWindow.g.h"
#include <winrt/Microsoft.Graphics.Canvas.UI.Xaml.h>
#include <winrt/Microsoft.UI.Xaml.Input.h>
#include <winrt/Microsoft.UI.Input.h>

namespace winrt::App4::implementation
{
    struct MainWindow : MainWindowT<MainWindow>
    {
        MainWindow();

        int32_t MyProperty();
        void MyProperty(int32_t value);
        float px, py;

        void CanvasControl_PointerMoved(winrt::Windows::Foundation::IInspectable const& sender, winrt::Microsoft::UI::Xaml::Input::PointerRoutedEventArgs const& e);
        void CanvasControl_Draw(winrt::Microsoft::Graphics::Canvas::UI::Xaml::CanvasControl const& sender, winrt::Microsoft::Graphics::Canvas::UI::Xaml::CanvasDrawEventArgs const& args);
    };
}

namespace winrt::App4::factory_implementation
{
    struct MainWindow : MainWindowT<MainWindow, implementation::MainWindow>
    {
    };
}
```

```
//MainWindow.xaml.cpp
using namespace winrt;
using namespace Microsoft::UI::Xaml;

// To learn more about WinUI, the WinUI project structure,
// and more about our project templates, see: http://aka.ms/winui-project-info.
using namespace winrt::Microsoft::Graphics::Canvas::UI::Xaml;
struct winrt::Windows::UI::Color col = winrt::Microsoft::UI::Colors::Green();
namespace winrt::App4::implementation
{
    MainWindow::MainWindow()
    {
        InitializeComponent();
        px = 200;
        py = 200;
    }

    int32_t MainWindow::MyProperty()
    {
        throw hresult_not_implemented();
    }

    void MainWindow::MyProperty(int32_t /* value */)
    {
        throw hresult_not_implemented();
    }
}


void winrt::App4::implementation::MainWindow::CanvasControl_PointerMoved(winrt::Windows::Foundation::IInspectable const& sender, winrt::Microsoft::UI::Xaml::Input::PointerRoutedEventArgs const& e)
{
    CanvasControl canvas = sender.as<CanvasControl>();
    px = e.GetCurrentPoint(canvas).Position().X;
    py = e.GetCurrentPoint(canvas).Position().Y;
    canvas.Invalidate();
}


void winrt::App4::implementation::MainWindow::CanvasControl_Draw(winrt::Microsoft::Graphics::Canvas::UI::Xaml::CanvasControl const& sender, winrt::Microsoft::Graphics::Canvas::UI::Xaml::CanvasDrawEventArgs const& args)
{
    auto drawingSession = args.DrawingSession();
    // 타원1
    drawingSession.DrawEllipse(px, py, 80, 60, col, 8);
    // 타원 안에 들어갈 텍스트
    drawingSession.DrawText(L"ANU", px - 25, py - 21, winrt::Microsoft::UI::Colors::Yellow());
    // 원 
    drawingSession.DrawEllipse(px + 100, py + 100, 40, 40, col, 4);
    // 직사각형 
    drawingSession.DrawRectangle(px + 150, py + 150, 80, 60, col, 4);
    // 원 안에 들어갈 텍스트
    drawingSession.DrawText(L"WIN2D", px + 80, py + 80, winrt::Microsoft::UI::Colors::Green());
    // 직사각형 안에 들어갈 텍스트
    drawingSession.DrawText(L"WINUI3", px + 150, py + 150, winrt::Microsoft::UI::Colors::Red());
}
```

실행 화면</br>
![Image description](./11.PNG)</br>
</br></br></br>
