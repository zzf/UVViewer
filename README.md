# UV Viewer for Unity Editor
UVViewerWindow 是一个编辑器窗口扩展类，允许您在 Unity 编辑器中查看网格的 UV。需要 Unity 5.4 或更高版本。

![](Screenshot.png)

## 安装
[发布页面]从 （https://github.com/songkyoo/UVViewer/releases） 下载和导入 unity 包，或将"Assets/Plugins"文件夹复制到项目中，UV 查看器将添加到菜单栏的Window->UI Viewer项中。运行该项时，将创建一个编辑器窗口。

## 用法
### 设置网格
如果网格条目为Selected Object，请选择包含Mesh或 MeshFilter、SkinnedMeshEnderer 组件的游戏对象以显示 UV。

如果将Mesh项设置为Custom，则可以自行设置网格。将对象拖放到视图区域中执行相同的行为。可拖动对象是包含Mesh或MeshFilter、SkinnedMeshEnderer组件的游戏对象。

### 纹理设置
如果Mesh条目为Selected Object，则如果选定的游戏对象包含MeshRenderer、SkinnedMeshRenderer组件，则如果Texture项设置为Material，则可以选择渲染器中包含的材质的纹理。

如果将Texture项设置为Custom，则可以自行设置纹理。将纹理拖放到视图区域中可以执行相同的操作。

### 从编辑器脚本访问
您可以设置由编辑器脚本创建的网格或纹理。下面的代码为窗口设置一个值，如果显示窗口，则在没有显示窗口时显示该窗口，则创建一个新窗口并设置一个值。

```csharp
using Macaron.UVViewer.Editor;

class EditorClass
{
    void SetCustom(Mesh mesh, Texture texture)
    {
        // 设置网格.
        UVViewerWindow.ShowWindow().SetCustomMesh(mesh);

        // 纹理设置.
        UVViewerWindow.ShowWindow().SetCustomTexture(texture);
    }
}
```

`SetCustomMesh`, `SetCustomTexture` 调用该方法时，Mesh、Texture条目将更改为Custom，而Source将设置为您调用的值。每个方法都可以单独调用。

## 局限性
1. 显示的 UV 和纹理不会自动反映对原始更改的更改。如果需要续订，则需要通过按网格体，纹理项目上的重新加载按钮来重新加载它。

2. 如果不支持几何着色器，则线粗条目不可用，并且视图区域在 HiDPI 环境中以低分辨率显示。
