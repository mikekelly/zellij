# Tab Index Display

This document describes the tab index display feature available in the `tab-bar` and `compact-bar` plugins.

## Overview

Both the `tab-bar` and `compact-bar` plugins support displaying numeric indices as prefixes on tab names. This makes it easier to identify tabs by their position and can be useful when switching tabs using keyboard shortcuts.

When enabled, tabs are displayed as:
```
1: Shell  2: Editor  3: Logs
```

Instead of:
```
Shell  Editor  Logs
```

## Configuration Options

### show_tab_index

- **Type:** boolean
- **Default:** `false`
- **Description:** When set to `true`, displays the tab position number as a prefix on each tab name.

### tab_index_offset

- **Type:** integer
- **Default:** `0`
- **Description:** An offset to apply to the displayed tab index. Useful if you want tabs to start from a number other than 1.

## Usage

### In a layout file

Configure the plugin in your layout file (`~/.config/zellij/layouts/my-layout.kdl`):

#### Using tab-bar (top bar)

```kdl
layout {
    pane size=1 borderless=true {
        plugin location="tab-bar" {
            show_tab_index true
            tab_index_offset 0
        }
    }
    pane
}
```

#### Using compact-bar (bottom bar)

```kdl
layout {
    pane
    pane size=1 borderless=true {
        plugin location="compact-bar" {
            show_tab_index true
            tab_index_offset 0
        }
    }
}
```

### Examples

#### Default indexing (1-based)

With `show_tab_index true` and `tab_index_offset 0` (default):

```
1: Shell  2: Editor  3: Logs
```

#### Zero-based indexing

With `show_tab_index true` and `tab_index_offset -1`:

```
0: Shell  1: Editor  2: Logs
```

#### Custom starting index

With `show_tab_index true` and `tab_index_offset 9`:

```
10: Shell  11: Editor  12: Logs
```

## Implementation

The feature is implemented in:
- `default-plugins/tab-bar/src/main.rs`
- `default-plugins/compact-bar/src/main.rs`

Both plugins read the configuration options during initialization and apply the index prefix when rendering tab names.
