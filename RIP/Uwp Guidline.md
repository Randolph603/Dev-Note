
## Icons

Reference:
- [**Microsoft Doc** - Icons for UWP apps](https://docs.microsoft.com/en-us/windows/uwp/design/style/icons)

> Use an icon for action and navigation.
> Use an icon if one already exists for the concept you want to represent.
> Use a predefined icon first, Microsoft provides [Segoe MDL2 Assets font](https://docs.microsoft.com/en-us/windows/uwp/design/style/segoe-ui-symbol-font), then use Vulcan font which could generate from [Icon8](https://icons8.com/).
> Use a Scalable Vector Graphics (SVG) file, not recommend a bitmap image, such as PNG, GIF, or JPEG

|				|Icon|Symbol|SymbolIcon|
|---------------|--|--|--|
| Button 		|  | |
| AppBarButton  |  | |


    <AppBarButton Icon="Like" Label="Like"/>
    <AppBarButton Label="Accept">
    <AppBarButton.Icon>
        <SymbolIcon Symbol="Accept" Foreground="Green"/>
    </AppBarButton.Icon>
    </AppBarButton>


UWP is dead!
RIP!