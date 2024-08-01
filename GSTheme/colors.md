# GSTheme colors

They are documented at https://developer.apple.com/documentation/appkit/nscolor/ui_element_colors?language=objc and https://developer.apple.com/design/human-interface-guidelines/color#macOS.

Thematic, ColorElement.m:53

```objc
      // This list should not be changed
      systemColorNames = [[NSArray alloc] initWithObjects:
        @"alternateRowBackgroundColor",
        @"alternateSelectedControlColor",
        @"alternateSelectedControlTextColor",
        @"controlBackgroundColor",
        @"controlColor",
        @"controlDarkShadowColor",
        @"controlHighlightColor",
        @"controlLightHighlightColor",
        @"controlShadowColor",
        @"controlTextColor",
        @"disabledControlTextColor",
        @"gridColor",
        @"headerColor",
        @"headerTextColor",
        @"highlightColor",
        @"keyboardFocusIndicatorColor", // Thematic said nameboard here, probably botched find-and-replace
        @"knobColor",
        @"rowBackgroundColor",
        @"scrollBarColor",
        @"secondarySelectedControlColor",
        @"selectedControlColor",
        @"selectedControlTextColor",
        @"selectedKnobColor",
        @"selectedMenuItemColor",
        @"selectedMenuItemTextColor",
        @"selectedTextBackgroundColor",
        @"selectedTextColor",
        @"shadowColor",
        @"textBackgroundColor",
        @"textColor",
        @"toolTipColor",
        @"toolTipTextColor",
        @"windowBackgroundColor",
        @"windowFrameColor",
        @"windowFrameTextColor",
        nil];

      /* Feel free to add extra colors here as they are added
       * in GSThemeDrawing.m
       */
      extraColorNames = [[NSArray alloc] initWithObjects:
        @"toolbarBackgroundColor",
        @"toolbarBorderColor",
        @"menuBackgroundColor",
        @"menuItemBackgroundColor",
        @"menuBorderColor",
        @"menuBarBackgroundColor",
        @"menuBarBorderColor",
        @"menuSeparatorColor",
        @"GSMenuBar",
        @"GSMenuBarTitle",
        @"tableHeaderTextColor",			  
        @"keyWindowFrameTextColor",
        @"normalWindowFrameTextColor",
        @"mainWindowFrameTextColor",
        @"windowBorderColor",
        @"browserHeaderTextColor",
        @"NSScrollView",
        @"highlightedTableRowBackgroundColor",
        @"highlightedTableRowTextColor",
        nil];
```