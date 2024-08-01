# KDE Color Scheme

The current color scheme can be found in `~/.config/kdeglobals`. Of particular interest are:

* `[General]AccentColor`, the raw accent color
* `[General]ColorScheme`, the base color scheme (which appears not to be defined in this file)

You can use `kreadconfig5` to read these values.

Colors are handled by the [`colors` KCM](https://invent.kde.org/plasma/plasma-workspace/-/tree/master/kcms/colors). [KColorScheme](https://api.kde.org/frameworks/kcolorscheme/html/classKColorScheme.html) is the API to read the color scheme, and describes what each of the categories and keys in kdeglobals means.

Mapping from kdeglobals keys to KColorScheme enums:

```c++
    constexpr std::array configMap = {
        std::pair{"ForegroundNormal", &SerializedColors::NormalText},
        std::pair{"ForegroundInactive", &SerializedColors::InactiveText},
        std::pair{"ForegroundActive", &SerializedColors::ActiveText},
        std::pair{"ForegroundLink", &SerializedColors::LinkText},
        std::pair{"ForegroundVisited", &SerializedColors::VisitedText},
        std::pair{"ForegroundNegative", &SerializedColors::NegativeText},
        std::pair{"ForegroundNeutral", &SerializedColors::NeutralText},
        std::pair{"ForegroundPositive", &SerializedColors::PositiveText},
        std::pair{"BackgroundNormal", &SerializedColors::NormalBackground},
        std::pair{"BackgroundAlternate", &SerializedColors::AlternateBackground},
    };
```

Some of them are [tints](https://invent.kde.org/frameworks/kguiaddons/-/blob/master/src/colors/kcolorutils.cpp?ref_type=heads#L113):

```c++
    // calculated backgrounds
    _brushes.bg[KColorScheme::ActiveBackground] =
        KColorUtils::tint(_brushes.bg[KColorScheme::NormalBackground].color(),
                          _brushes.fg[KColorScheme::ActiveText].color());
    _brushes.bg[KColorScheme::LinkBackground] =
        KColorUtils::tint(_brushes.bg[KColorScheme::NormalBackground].color(),
                          _brushes.fg[KColorScheme::LinkText].color());
    _brushes.bg[KColorScheme::VisitedBackground] =
        KColorUtils::tint(_brushes.bg[KColorScheme::NormalBackground].color(),
                          _brushes.fg[KColorScheme::VisitedText].color());
    _brushes.bg[KColorScheme::NegativeBackground] =
        KColorUtils::tint(_brushes.bg[KColorScheme::NormalBackground].color(),
                          _brushes.fg[KColorScheme::NegativeText].color());
    _brushes.bg[KColorScheme::NeutralBackground] =
        KColorUtils::tint(_brushes.bg[KColorScheme::NormalBackground].color(),
                          _brushes.fg[KColorScheme::NeutralText].color());
    _brushes.bg[KColorScheme::PositiveBackground] =
        KColorUtils::tint(_brushes.bg[KColorScheme::NormalBackground].color(),
                          _brushes.fg[KColorScheme::PositiveText].color());
```

## Notifying changes

### KGlobalSettings (apparently deprecated)

* <https://invent.kde.org/plasma/plasma-workspace/-/blob/master/kcms/kcms-common_p.h#L37>

```c
enum GlobalChangeType {
    PaletteChanged = 0,
    FontChanged,
    StyleChanged, // 2
    SettingsChanged,
    IconChanged,
    CursorChanged, // 5
    ToolbarStyleChanged,
    ClipboardConfigChanged,
    BlockShortcuts,
    NaturalSortingChanged,
};

void notifyKcmChange(GlobalChangeType changeType, int arg)
{
    QDBusMessage message =
        QDBusMessage::createSignal(QStringLiteral("/KGlobalSettings"), QStringLiteral("org.kde.KGlobalSettings"), QStringLiteral("notifyChange"));
    message.setArguments({changeType, arg});
    QDBusConnection::sessionBus().send(message);
}
```

## Watching changes

### KConfigWatcher

* <https://invent.kde.org/frameworks/kconfig/-/blob/master/src/core/kconfigwatcher.cpp>

### Just use inotify

This seems like the most reliable solution -- just set up an inotify watch on `~/.config/kdeglobals`

## Reading the file

Use an INI parser such as [`inih`](https://github.com/benhoyt/inih) or [`libconfini`](https://github.com/madmurphy/libconfini).