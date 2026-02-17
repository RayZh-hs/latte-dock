# Plasma 6 Port — Remaining Work

## Done ✅
- Unversioned QML module imports (taskmanager, activities, etc.)
- `plasmoid.action()` → `plasmoid.internalAction()` (all call sites)
- Connections signal syntax (`function onSignalName()`)
- Panel.qml location signal workaround
- VisibilityManager null guards
- CompactApplet.qml (mSize, tooltip nulls)
- `theme`/`units` fixes in startup-critical path (~28 files)
- Additional Plasma 6 migration pass completed:
    - `TaskIcon.qml` (`theme.*` → `Kirigami.Theme.*`)
    - `Ruler.qml` (`theme.defaultFont.*` → `Qt.application.font.*`)
    - `EffectsConfig.qml` (`theme.*`/`units.*` → `Kirigami.Theme.*`/`Kirigami.Units.*`)
    - indicators default `config.qml` (`theme.*`/`units.*` → `Kirigami.Theme.*`/`Kirigami.Units.*`)
    - `TypeSelection.qml` (`theme.defaultFont.*`/`units.*` migrated)
    - `AppletDelegate.qml` (`theme.*`/`units.*` migrated)
- Additional Plasma 6 migration pass completed (2026-02-17):
    - `LatteDockConfiguration.qml` (core `theme.*`/`units.*` usage migrated to `Kirigami.Theme.*`/`Kirigami.Units.*`)
    - `ProgressOverlay.qml` (`theme.*` migrated to `Kirigami.Theme.*`)
    - `ComboBox.qml` (key `units.*` and active `theme.*` references migrated)
    - `LatteDockSecondaryConfiguration.qml`, `DragCorner.qml`, `main.qml`, `SubHeader.qml`, `Header.qml` (remaining low-risk refs migrated)
- Build succeeds

## Remaining: bare `theme.` refs → Kirigami.Theme (~85 hits)
- `theme.textColor/backgroundColor/highlightColor/etc` → `Kirigami.Theme.*`
- `theme.buttonFocusColor` → `Kirigami.Theme.focusColor`
- `theme.mSize(theme.defaultFont).width/height` → `Kirigami.Units.gridUnit`
- `theme.defaultFont.pixelSize/pointSize` → `Qt.application.font.*`
- `theme.smallestFont` → `Kirigami.Theme.smallFont`
- Heaviest files now: AppearanceConfig.qml(26), LatteDockConfiguration.qml(7),
    ProgressOverlay.qml(6), ComboBox.qml(5), indicators plasma config.qml(4)

## Remaining: bare `units.` refs → Kirigami.Units (~187 hits)
- `units.smallSpacing/gridUnit/largeSpacing/iconSizes.*` → `Kirigami.Units.*`
- Heaviest: TasksConfig(39), BehaviorConfig(37), AppearanceConfig(34),
    LatteDockConfiguration(25), Slider(7), ComboBox(6)

## Current snapshot
- Remaining bare refs total (`theme.` + `units.`): **210**

## Other potential issues (untested)
- Verify `PlasmaCore.Types.*` enums still resolve (may need PlasmaCore→KSvg)
- `PlasmaCore.FrameSvgItem` usage — some may need `KSvg.FrameSvgItem`
- `PlasmaComponents.ContextMenu` was removed in Plasma 6 (ContextMenu.qml)
- `org.kde.draganddrop` may be removed — check runtime
- `Qt5Compat.GraphicalEffects` works but is a compat shim
- KQuickControlsAddons usage may need updating
- `QtQuick.Controls 1.4` imports are deprecated (TextField.qml, etc.)
- Test full runtime: tooltips, context menus, edit mode, drag-drop, indicators
