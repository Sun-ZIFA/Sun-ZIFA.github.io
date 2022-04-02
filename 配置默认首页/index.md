# 配置默认首页




> 💡 在WPF应用程序+Prism框架中，一般都是使用Navigation导航进行区域页面的切换，当我配置默认首页的时候出现了一些问题，所以这里来记录一下

<br/>
配置默认首页的时候，我一开始的想法就是在构造函数中进行导航到首页

```csharp
public class MainViewModel
{
		public MainViewModel(IRegionManager regionManager)
		{
				regionManager.Regions["regionManager"].RequestNavigate("IndexView");
		}
}
```
<br/>
但是在元素的构造函数被调用时，元素的很多属性都没准备好，就例如ContentControl中区域部分，从而导致异常，The region manager does not contain the regionManager region.
&nbsp
这时候就要去程序入口App.xaml.cs重写OnInitialized这个方法，如下

```csharp
//App.xaml.cs
protected override void OnInitialized()
{
	   var service = App.Current.MainWindow.DataContext as IConfigService;
	   if(service != null)
     {
				//去执行Configure方法
        service.Configure();
     }
     base.OnInitialized();
}  
```
<br/>
这里使用了IConfigService接口存放程序初始配置项

```csharp
//IConfigService.cs
public interface IConfigService
{
    void Configure();
}
```
<br/>
继承IConfigService接口，实现Configure方法去进行导航切换

```csharp
public class MainViewModel : IConfigService
{
		private readonly IRegionManager regionManager;
		public MainViewModel(IRegionManager regionManager)
		{
				this.regionManager = regionManager;
		}

		public void Configure()
    {
        regionManager.Regions["regionManager"].RequestNavigate("IndexView");
    }
}
```
