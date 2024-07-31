# KDE Color Scheme

The current color scheme can be found in `~/.config/kdeglobals`. Of particular interest are:

* `[General]AccentColor`, the raw accent color
* `[General]ColorScheme`, the base color scheme (which appears not to be defined in this file)

You can use `kreadconfig5` to read these values.

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