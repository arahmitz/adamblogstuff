---
title: "Tools"
date: 2026-01-15T18:00:00+01:00
draft: false

showDate : false
showDateOnlyInArticle : false
showDateUpdated : false
showHeadingAnchors : false
showPagination : false
showReadingTime : false
showTableOfContents : false
showTaxonomies : false 
showWordCount : false
showSummary : false
sharingLinks : false
showEdit: false
showViews: false
showLikes: false
showAuthor: false
layoutBackgroundHeaderSpace: false
heroStyle: background
---
**madTools** is a collection of Maya tools I've written that I use everyday. Since I started learning animation, I've used many awesome tools from many awesome developers and I've always wanted to do the same. Feel free to use, share and edit.

To keep everything up to date, clone [the repository](https://github.com/arahmitz/madTools).
{{< github repo="arahmitz/madtools" showThumbnail=false >}}

You can install a shelf, use the provided UI or download the tools you want individually below - name links to direct script.


## Tools
| Icon | Download | Desciption                                   |
|------|----------|----------------------------------------------|
| <div style="display:flex; align-items:center;"><img src="https://github.com/arahmitz/madTools/blob/main/madtools/icons/create_joints.png?raw=true" width="32" height="32"> | [Create Joints](https://raw.githubusercontent.com/arahmitz/madTools/refs/heads/main/madtools/tools/create_joints.py)| Creates a joint chain in +X with editable number of joints, spacing, and naming (via command or UI)|
| <div style="display:flex; align-items:center;"><img src="https://github.com/arahmitz/madTools/blob/main/madtools/icons/create_locator.png?raw=true" width="32" height="32"></div> | [Create Locator](https://raw.githubusercontent.com/arahmitz/madTools/refs/heads/main/madtools/tools/create_locator.py)| Creates a locator at you current selection (or origin if nothing is selected) |
| <div style="display:flex; align-items:center;"><img src="https://github.com/arahmitz/madTools/blob/main/madtools/icons/snap_to_average.png?raw=true" width="32" height="32"></div> | [Snap to Average](https://raw.githubusercontent.com/arahmitz/madTools/refs/heads/main/madtools/tools/snap_to_average.py) | Snaps last selected objects to average of the rest **(translation & rotation)** |
| <div style="display:flex; align-items:center;"><img src="https://github.com/arahmitz/madTools/blob/main/madtools/icons/point_to_average.png?raw=true" width="32" height="32"></div>| [Point to Average](https://raw.githubusercontent.com/arahmitz/madTools/refs/heads/main/madtools/tools/point_to_average.py) | Snaps last selected object to average of the rest **(translation only)** |
| <div style="display:flex; align-items:center;"><img src="https://github.com/arahmitz/madTools/blob/main/madtools/icons/snap_to_parent.png?raw=true" width="32" height="32"></div> | [Snap To Parent](https://raw.githubusercontent.com/arahmitz/madTools/refs/heads/main/madtools/tools/snap_to_parent.py) | Snaps **all** selected objects to the first selected object **(translation & rotation)** |
| <div style="display:flex; align-items:center;"><img src="https://github.com/arahmitz/madTools/blob/main/madtools/icons/freeze_transforms.png?raw=true" width="32" height="32"></div> |[Freeze Transforms](https://raw.githubusercontent.com/arahmitz/madTools/refs/heads/main/madtools/tools/freeze_transforms.py) | Freezes transformations |
| <div style="display:flex; align-items:center;"><img src="https://github.com/arahmitz/madTools/blob/main/madtools/icons/select_hierarchy.png?raw=true" width="32" height="32"></div> | [Select Hierarchy](https://raw.githubusercontent.com/arahmitz/madTools/refs/heads/main/madtools/tools/select_hierarchy.py)| Selects the full hierarchy of the selected object |
| <div style="display:flex; align-items:center;"><img src="https://github.com/arahmitz/madTools/blob/main/madtools/icons/delete_history.png?raw=true" width="32" height="32"></div> | [Delete History](https://raw.githubusercontent.com/arahmitz/madTools/refs/heads/main/madtools/tools/delete_history.py)| Deletes history via `Delete History` -> `By Type` |
| <div style="display:flex; align-items:center;"><img src="https://github.com/arahmitz/madTools/blob/main/madtools/icons/toggle_lra.png?raw=true" width="32" height="32"></div> | [Toggle LRA](https://raw.githubusercontent.com/arahmitz/madTools/refs/heads/main/madtools/tools/toggle_lra.py)| Toggles selected object's Local Rotation Axis on/off |
| <div style="display:flex; align-items:center;"><img src="https://github.com/arahmitz/madTools/blob/main/madtools/icons/joint_zso.png?raw=true" width="32" height="32"></div> | [Joint ZSO](https://raw.githubusercontent.com/arahmitz/madTools/refs/heads/main/madtools/tools/joint_zso.py) | Matches rotation axis to translation axis via `joint -e -zso` |
| <div style="display:flex; align-items:center;"><img src="https://github.com/arahmitz/madTools/blob/main/madtools/icons/make_rom.png?raw=true" width="32" height="32"></div> | [Make ROM](https://raw.githubusercontent.com/arahmitz/madTools/refs/heads/main/madtools/tools/make_rom.py) | Creates keyframes on all selected objects every 10 frames from the current `startTime` to current `endTime` to help with creation of Range of Motion animation | 
