# Plasma 6 Port — Remaining Work

## Done ✅
- Unversioned QML module imports (taskmanager, activities, etc.)
- `plasmoid.action()` → `plasmoid.internalAction()` (all call sites)
- Connections signal syntax (`function onSignalName()`)
- Panel.qml location signal workaround
- VisibilityManager null guards
- CompactApplet.qml (mSize, tooltip nulls)
- `theme`/`units` fixes in startup-critical path (~28 files)
- Build succeeds

## Remaining: bare `theme.` refs → Kirigami.Theme (~117 hits, 32 files)
- `theme.textColor/backgroundColor/highlightColor/etc` → `Kirigami.Theme.*`
- `theme.buttonFocusColor` → `Kirigami.Theme.focusColor`
- `theme.mSize(theme.defaultFont).width/height` → `Kirigami.Units.gridUnit`
- `theme.defaultFont.pixelSize/pointSize` → `Qt.application.font.*`
- `theme.smallestFont` → `Kirigami.Theme.smallFont`
- Heaviest files: AppearanceConfig.qml(26), Ruler.qml(13),
  indicators config.qml(10), EffectsConfig.qml(7), TaskIcon.qml(4)

## Remaining: bare `units.` refs → Kirigami.Units (~221 hits, 29 files)
- `units.smallSpacing/gridUnit/largeSpacing/iconSizes.*` → `Kirigami.Units.*`
- Heaviest: TasksConfig(39), BehaviorConfig(36), AppearanceConfig(34),
  LatteDockConfiguration(24), EffectsConfig(19), AppletDelegate(7)

## Other potential issues (untested)
- Verify `PlasmaCore.Types.*` enums still resolve (may need PlasmaCore→KSvg)
- `PlasmaCore.FrameSvgItem` usage — some may need `KSvg.FrameSvgItem`
- `PlasmaComponents.ContextMenu` was removed in Plasma 6 (ContextMenu.qml)
- `org.kde.draganddrop` may be removed — check runtime
- `Qt5Compat.GraphicalEffects` works but is a compat shim
- KQuickControlsAddons usage may need updating
- `QtQuick.Controls 1.4` imports are deprecated (TextField.qml, etc.)
- Test full runtime: tooltips, context menus, edit mode, drag-drop, indicators
