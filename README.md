## binding-reactive-mvvm-accordion-xamarin

This sample demonstrates how to bind item sources using Reactive MVVM with Syncfusion's SfAccordion control in a Xamarin.Forms project. The sample wires a ReactiveUI view model into a XAML page that hosts an `SfAccordion` where each `AccordionItem` shows a grouped list using `SfListView`. 

To learn more about SfAccordion, check out the official user guide topics:

- [Getting Started with Xamarin Accordion (SfAccordion)](https://help.syncfusion.com/xamarin/accordion/getting-started)

**KB Link:** **[View document in Syncfusion Xamarin Knowledge base](https://www.syncfusion.com/kb/12180/how-to-bind-itemsource-using-reactive-mvvm-in-xamarin-forms-accordion-sfaccordion)**

## Overview

In this example:

- The page is a `ReactiveContentPage<TViewModel>` from ReactiveUI.XamForms and receives its `ViewModel` via constructor injection.
- The `SfAccordion` control is bound to a collection (`Contacts`) on the view model using `BindableLayout.ItemsSource`.
- Each accordion item contains a header and a content area. The content area uses `Syncfusion.ListView` (`SfListView`) to render child contacts. The `TapGestureRecognizer` on each child forwards taps to a command on the page's binding context.

## XAML
```
<syncfusion:SfAccordion x:Name="Accordion" BindableLayout.ItemsSource="{Binding Contacts}" ExpandMode="SingleOrNone" >
    <BindableLayout.ItemTemplate>
        <DataTemplate>
            <syncfusion:AccordionItem  >
                <syncfusion:AccordionItem.Header >
                    <Grid HeightRequest="60">
                        <Label Text="{Binding Type}" BackgroundColor="Aqua" VerticalTextAlignment="Center" HorizontalTextAlignment="Center"/>
                    </Grid>
                </syncfusion:AccordionItem.Header>
                <syncfusion:AccordionItem.Content>
                    <Grid x:Name="mainGrid" Padding="4" HeightRequest="135" >
                        <sflistview:SfListView AllowGroupExpandCollapse="True" IsScrollingEnabled="False" x:Name="listView" IsScrollBarVisible="False" AutoFitMode="DynamicHeight"
                        ItemSpacing="3" ItemsSource="{Binding Contacts}" >
                            <sflistview:SfListView.ItemTemplate>
                                <DataTemplate>
                                    <Grid HeightRequest="60" Padding="1" >
                                        <Label Text="{Binding ContactName}" BackgroundColor="LightBlue"/>
                                        <Grid.GestureRecognizers>
                                            <TapGestureRecognizer Command="{Binding Path=BindingContext.TapCommand, Source={x:Reference Accordion}}" CommandParameter="{Binding .}" />
                                        </Grid.GestureRecognizers>
                                    </Grid>
                                </DataTemplate>
                            </sflistview:SfListView.ItemTemplate>
                        </sflistview:SfListView>
                    </Grid>
                </syncfusion:AccordionItem.Content>
            </syncfusion:AccordionItem>
        </DataTemplate>
    </BindableLayout.ItemTemplate>
</syncfusion:SfAccordion>
```

## C#
```
    public partial class MainPage : ReactiveContentPage<ViewModel>
    {
        public MainPage(ViewModel viewModel)
        {
            ViewModel = viewModel;
            InitializeComponent();
        }
    }
```

## How it works

- ReactiveUI integration: The view inherits from `ReactiveContentPage<T>` so it can access reactive bindings and commands easily.
- Accordion binding: `BindableLayout.ItemsSource` binds the `Contacts` collection on the view model to create one `AccordionItem` per group.
- Nested list: Each accordion item content contains an `SfListView` bound to the group's `Contacts` collection to display members.
- Commands: The child list item uses a `TapGestureRecognizer` that targets `TapCommand` on the `Accordion` page's `BindingContext` so tapping an item raises a view-model command with the tapped item as parameter.

##### Conclusion
I hope you enjoyed learning about how to bind ItemSource using Reactive MVVM in Xamarin.Forms Accordion (SfAccordion)

You can refer to our  [Xamarin.Forms Accordion feature tour](https://www.syncfusion.com/xamarin-ui-controls/xamarin-accordion) page to know about its other groundbreaking feature representations and [documentation](https://help.syncfusion.com/xamarin/accordion/getting-started), and how to quickly get started for configuration specifications. You can also explore our [Xamarin.Forms Accordion example](https://www.syncfusion.com/demos/xamarin) to understand how to create and manipulate data.

For current customers, you can check out our Document Processing Libraries from the [License and Downloads](https://www.syncfusion.com/account/login) page. If you are new to Syncfusion, you can try our 30-day [free trial](https://www.syncfusion.com/downloads) to check out our controls.

If you have any queries or require clarifications, please let us know in the comments section below. You can also contact us through our [support forums](https://www.syncfusion.com/forums) or [Direct-trac](https://support.syncfusion.com/create). We are always happy to assist you!


