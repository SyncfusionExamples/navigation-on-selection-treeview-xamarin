# How to do navigation on selection in Xamarin.Forms TreeView (SfTreeView)

You can navigate to another page by selecting the [TreeViewNode](https://help.syncfusion.com/cr/cref_files/xamarin/Syncfusion.SfTreeView.XForms~Syncfusion.TreeView.Engine.TreeViewNode.html) in Xamarin.Forms [SfTreeView](https://help.syncfusion.com/xamarin/treeview/overview) by binding [SelectedItem](https://help.syncfusion.com/cr/xamarin/Syncfusion.SfTreeView.XForms~Syncfusion.XForms.TreeView.SfTreeView~SelectedItem.html) property from **ViewModel**.

**XAML**

Binding ViewModel **TreeViewSelectedItem** to **SfTreeView.SelectedItem**.

``` xml
ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:TreeViewXamarin"
             xmlns:syncfusion="clr-namespace:Syncfusion.XForms.TreeView;assembly=Syncfusion.SfTreeView.XForms"
             x:Class="TreeViewXamarin.MainPage">
    <ContentPage.BindingContext>
        <local:FileManagerViewModel x:Name="viewModel"/>
    </ContentPage.BindingContext>
    <ContentPage.Content>
        <syncfusion:SfTreeView x:Name="treeView" ChildPropertyName="SubFiles" SelectedItem="{Binding TreeViewSelectedItem, Mode=TwoWay}" ExpandActionTarget="Node" ItemTemplateContextType="Node" AutoExpandMode="None" ItemsSource="{Binding ImageNodeInfo}">
            <syncfusion:SfTreeView.ItemTemplate>
                <DataTemplate>
                    <Grid x:Name="grid" RowSpacing="0" >
                        <Grid.ColumnDefinitions>
                            <ColumnDefinition Width="40" />
                            <ColumnDefinition Width="*" />
                        </Grid.ColumnDefinitions>
                        <Image Source="{Binding Content.ImageIcon}" VerticalOptions="Center" HorizontalOptions="Center" HeightRequest="35" WidthRequest="35"/>
                        <Grid Grid.Column="1" RowSpacing="1" Padding="1,0,0,0" VerticalOptions="Center">
                            <Label LineBreakMode="NoWrap" Text="{Binding Content.ItemName}" VerticalTextAlignment="Center"/>
                        </Grid>
                    </Grid>
                </DataTemplate>
            </syncfusion:SfTreeView.ItemTemplate>
        </syncfusion:SfTreeView>
    </ContentPage.Content>
</ContentPage>
```

**C#**

Navigate to another page in the ViewModel **TreeViewSelectedItem** setter using [PushAsync](https://docs.microsoft.com/en-us/dotnet/api/xamarin.forms.inavigation.pushasync) method.

``` c#
namespace TreeViewXamarin
{
    public class FileManagerViewModel
    {
        private FileManager treeViewSelectedItem;

        public FileManager TreeViewSelectedItem
        {
            get { return treeViewSelectedItem; }
            set
            {
                if (treeViewSelectedItem != value)
                {
                    treeViewSelectedItem = value;
                    ItemSelected(treeViewSelectedItem);
                }
            }
        }

        private async void ItemSelected(FileManager selectedItem)
        {
            await Task.Delay(250);
            var newPage = new NewPage();
            newPage.BindingContext = selectedItem;
            await App.Current.MainPage.Navigation.PushAsync(newPage);
        }
    }
}
```

**Output**

![NavigationOnSelection](https://github.com/SyncfusionExamples/navigation-on-selection-treeview-xamarin/blob/master/ScreenShot/NavigationOnSelection.gif)
