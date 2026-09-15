# Layout AI Agent — User Guide

**SynerRaise · Early Access · September 15, 2026**

[Download HTML guide](user-guide.html) — save the HTML file and open it in a browser. Use Print → Save as PDF for a printable copy.

## Read this first

Layout AI Agent (Lagent) is developed and published by SynerRaise. This guide covers the current Early Access interface, reviewed September 15, 2026. Commands may differ in older builds; use Help > About to identify your version and the built-in Help for that build.

- The publicly available trial is for Windows x86-64. This guide does not certify macOS or Linux releases.
- Use this application for GDSII viewing, inspection, measurement, and basic editing. It is not a signoff verification tool.
- The native OA-like format is application-specific and does not provide Cadence OpenAccess interoperability.
- Download the installer from the official public releases page, compare its SHA-256 checksum with the release checksum, and run it for the current Windows user. The Early Access installer is unsigned.
- Keep the original GDS unchanged. Save edits to a separate native project, export to a new GDS path, and reopen the export to inspect it before external verification.

## Getting Started

Create a layout, open a native database, or import a GDS stream, then choose the cell you want to view.

- Use File > New Layout to start a document, Open OA Database for a native project, or Stream > In GDS to import GDSII.
- Select a cell in the Cells panel. Press F or use Fit View to center its complete bounding box.
- Choose Edit mode when changes are required, or View-only mode for protected inspection.

![Welcome screen: choose New Layout, Open OA Database, or Stream In GDS to begin.](images/welcome.png)

*Welcome screen: choose New Layout, Open OA Database, or Stream In GDS to begin.*

## Files & Documents

Native documents and GDS streams have different save behavior.

- Save updates the active native document. An imported GDS uses Save As until a native destination is selected.
- Stream Out writes either the complete library or a selected root cell and its referenced hierarchy to GDS.
- The title and status bar indicate the active file, current mode, dirty state, and operation progress.

## Pan & Zoom

Use direct canvas controls for detailed inspection without changing layout data.

- Zoom with the mouse wheel, toolbar buttons, Ctrl++ or Ctrl+-, and keep the pointer over the area of interest.
- Use Zoom Box to drag a region to fit; a single primary click zooms in at the pointer.
- Pan with the middle or secondary mouse button. Arrow keys navigate the viewport; F fits the active cell.

![Full-layout overview: Cells on the left, canvas in the center, and layer controls on the right. Press F or F2 to fit the active view.](images/layout-overview.png)

*Full-layout overview: Cells on the left, canvas in the center, and layer controls on the right. Press F or F2 to fit the active view.*

## Selection

Select one or many direct objects and instances in the active cell.

- Activate Select and click a direct shape, path, visible text label, node, or instance. Check the status bar for its cell, element kind, and index.
- Drag a selection box to select multiple objects. Hold Shift to add matches or Ctrl to remove matches.
- Use Edit > Selection > All Objects to select every direct object. After a click finds overlapping objects, press Space or Shift+Space to cycle through them.
- Use Edit > Selection > Move By for an exact dx/dy offset in the current display unit. It moves the complete selection as one undoable edit.
- Use Edit > Selection > Move To to place the selection's lower-left bounds at an absolute coordinate in the current display unit.
- Use Change Layer to assign selected layer-bearing objects to another layer/datatype, or Area and Perimeter to measure selected Boundary, Box, and Path objects.
- Use Edit > Selection > Transform to rotate or mirror the complete selection around its shared center. Each command creates one undo step.
- Use Transform > Arbitrary Transform for entered-angle rotation and scaling. Choose a selection-center, lower-left, or custom origin; Preview is non-mutating and Apply creates one undo step.
- Use Transform > Flatten Instances to replace selected SREF/AREF instances with transformed child contents through an entered hierarchy depth. Layers, element properties, and inherited instance properties are retained.
- Use Transform > Resolve Arrays to replace selected AREFs with equivalent SREF placements. A safety limit prevents accidental generation of more than one million objects.
- Use Make Cell to extract the selection into a uniquely named cell and replace it with one SREF at the selection's original lower-left coordinate.
- Use Make Array on exactly one SREF to create a rectangular AREF. Rows and columns must be positive; spacing uses the current display unit and repeated axes require non-zero spacing.
- Use Shapes > Size Shapes to grow or inset selected Boundary/Box geometry. Use Shapes > Merge Shapes to union touching or overlapping selections; different layer/datatype pairs remain separate and hole topology is retained.
- For Shapes > Boolean, the primary selection is the subject and additional selections are operands. All must share one cell and layer/datatype. Union and XOR are symmetric; Intersection and Subtract Operands from Subject evaluate the primary subject against the combined operands; Separate Overlaps emits non-overlapping atomic regions.
- Use Edit > Selection > Align with at least two selected objects. The primary selection remains fixed and all secondary objects move as one undoable edit.
- Use Edit > Selection > Distribute with at least three selected objects. The geometric outer pair stays fixed while intermediate objects receive equal gaps or equal center spacing.
- Use Edit > Search Objects and choose Visible Hierarchy to find the descendant geometry shown on the canvas, Active Cell Only for directly editable objects, or Entire Hierarchy to ignore the display-depth limit. The Visible Hierarchy label reports Level N or Full. Changing scope clears the prior results; press Search to populate the new scope. Changed filters or display depth mark old rows outdated until Search is pressed.
- Selection includes only visible layers and visible Text. Hiding a layer or disabling View > Text removes affected objects from the current selection.
- Press Shift+F2 or use Display > Fit Selection to center selected geometry, text, and transformed instances.
- Switch to Move in Edit mode to drag the selection, or use arrow keys. Delete removes selected objects and Ctrl+Z restores them.

## Search Objects

Find layout objects by geometry, layer, label, or referenced-cell criteria without modifying the document.

- Open Edit > Search Objects. Choose Active Cell Only for direct editable objects, Visible Hierarchy for the descendants currently displayed, or Entire Hierarchy to search beyond the display-depth limit.
- Set Type, Layer, or Datatype as needed. Text Contains matches label content; Referenced Cell matches only the target name of SREF and AREF instances, not geometry stored inside that cell.
- Changing Scope clears the prior results and highlights so they cannot be mistaken for matches in the new scope. Press Search after choosing the scope or changing a filter. If the hierarchy display depth changes, existing Visible Hierarchy results are marked outdated until refreshed.
- Read Hierarchy Path to identify the placed occurrence. Scope reports Direct for active-cell objects and Child for descendant occurrences; the summary gives separate direct and descendant totals.
- Choose a row and use Select to highlight it or Fit to center it. Select All Results highlights the bounded result set. Search remains modeless, so the canvas can still be panned or zoomed outside the dialog.
- Results truncated means additional matches exist beyond the 2,000 displayed rows. Search incomplete means the guarded definition scan stopped early, so even zero displayed results are not a definitive no-match answer.

## Properties

Inspect or edit object, ruler, and cell data through one staged dialog.

- Select an object or ruler and press Q. If the canvas selection is empty, select a cell in the Cells panel and press Q for cell information.
- Review layer, datatype, geometry, placement, transformation, reference, measurement, or user-property fields appropriate to the target.
- Use Previous and Next for a multi-selection. Apply commits without closing; OK commits and closes; Cancel discards staged edits.
- Apply to Same Type copies compatible edited fields while preserving each target's own geometry, placement, and reference identity.

## Cell Hierarchy

Control how much hierarchy is drawn and navigate through referenced cells.

- Use Full Detail, Root Box, Top Level, More Detail, and Less Detail to control hierarchy expansion.
- Enable Instance Labels to show direct instance boxes and names, then select an instance and press Ctrl+D to descend.
- Choose Child selects an immediate child explicitly. Ascend, Parent, Back, and Forward restore navigation context.

## Locate Cell Instances

Highlight every placement of a chosen cell within the currently displayed hierarchy.

- Right-click the desired cell in the Cells panel and choose Locate Instances to draw labeled amber boxes around its placements.
- Choose Locate and Fit to highlight the placements and fit their combined bounds in one action.
- Use Clear Highlights from the cell context menu, or press Escape, to remove the locator overlay.
- Locating is an on-demand view operation: it does not select, edit, or retessellate the layout geometry.

## Editing Tools

Edit mode provides native geometry creation and modification tools.

- Polygon and Path accept point clicks and finish with double-click, secondary click, or Enter; Box uses a drag gesture.
- Live previews show segment measurements for Polygon and Path, and width, height, and diagonal for Box. Toggle them with the toolbar's 123 dimension button.
- Text places a label with content, magnification, and angle. Instance places a cell reference or configured array.
- Partial edits the vertices of supported geometry. Tool Options shows inputs for the active tool; Escape cancels unfinished work.
- Copy and Cut operate on the complete direct-object selection. Ctrl+V starts an overlay preview that follows the snapped pointer; click once to commit or use Escape/secondary-click to cancel.
- Use Paste in Place (Ctrl+Shift+V) to retain original coordinates. Paste, Paste in Place, and Duplicate each commit as one undoable edit with one geometry refresh.

## Rulers, Grid & Units

Measurement and snapping tools improve placement accuracy without changing display scale.

- Ruler uses two points or drag-and-release. Shift constrains orthogonally and Ctrl constrains to 45-degree angles.
- Select an existing ruler and press Delete to remove it, or use Edit > Clear All Rulers.
- Enable Snap to Grid and choose automatic or fixed spacing. Display Unit switches editor values between DBU and nanometers.

## Layers & Styles

The Layers panel controls participation and the Layer Tools area controls presentation.

- Right-click a row or empty list area and choose New Layer to add a layer/datatype pair to an editable document.
- Select a layer row to make it active, use its checkbox to show or hide it, and use All or None for bulk visibility.
- Adjust fill color, frame color, fill, frame, opacity, stipple, and line style in Layer Tools.
- Use Edit > Layer > Clear Layer to remove geometry but retain the active layer definition. Delete Layer removes both geometry and its display definition; Copy Layer duplicates all source-layer geometry across the library.
- Load or save .lyp layer properties from File. Saved properties preserve the application's visible style settings.

![Detailed layout view: select a layer on the right, then adjust colors and stipple in the Layer Toolbox below. Display colors are presentation settings, not electrical verification results.](images/layout-detail.png)

*Detailed layout view: select a layer on the right, then adjust colors and stipple in the Layer Toolbox below. Display colors are presentation settings, not electrical verification results.*

## Cells & Reports

Maintain cell definitions and inspect document-level information without navigating away from the canvas.

- Use Edit > Cell > Rename Cell to rename the active cell; SREF and AREF targets are updated throughout the library.
- Delete Cell protects referenced cells. Remove or retarget every reported dependent instance before deleting that cell; the only remaining cell cannot be deleted.
- Use File > Layout Statistics to review structure, top-cell, layer/datatype, element-type, and active-view bounds information.
- Use File > Screenshot to File to save the current canvas as PNG, or Screenshot to Clipboard to paste it into another application. Complex views wait for progressive layer preparation to complete before capture.

## View & Display

View controls interface and drawing aids; Display controls hierarchy and canvas navigation.

- View toggles grid, text, cell frames, missing references, wireframe rendering, and docked panels.
- Use F3 to show or hide Tool Options. The toolbar, Cells panel, Layers panel, and Layer Tools can be toggled independently.
- Display provides fit, redraw, position navigation, instance labels, hierarchy depth, and display history.
- Use Display > Global Orientation to rotate the complete presentation in 90-degree steps, mirror it at the X axis, or reset it. This does not modify stored GDS coordinates or geometry.
- Enable View > Navigator to show an isolated bounds-only minimap. Its amber rectangle tracks the current viewport; click inside the minimap to recenter the canvas.

## Bookmarks, Recent Files & Session

Return to review locations and resume the application without rebuilding your workspace manually.

- Use View > Bookmarks > Add View Bookmark, enter a name, and choose Add. Reusing a name updates that bookmark.
- A bookmark restores its document, active cell, hierarchy depth, viewport scale and offset, global rotation and mirroring, active layer, and visible-layer set. Choosing a bookmark for another document opens that document first; a bookmark never changes layout geometry.
- File > Recent identifies GDS, native projects, and layer-property files by type. Hover an entry for its complete path. Missing paths are removed when selected; Clear Recent Files removes the list but does not delete files.
- Normal exit stores the open document reference plus panel and display preferences. Enable View > Restore Previous Document at Startup to reopen that document and restore its saved view on the next normal GUI launch; this option is off by default. An explicit command-line GDS path always takes precedence.
- Session data is application configuration, not part of the GDS or native project. Unsaved geometry still requires Save or Stream Out before exit.
- Use View > Navigator for a movable and resizable overview. The amber rectangle represents the main canvas viewport; click within the layout bounds to recenter. Navigator uses cached bounds and remains independent of main-layout rendering.

## Save & Recovery

Background persistence protects the interface and stages writes before replacing a valid destination.

- Wait for the save progress dialog to complete, or cancel before the destination replacement stage when cancellation is available.
- If edits occur during a background save, the document remains marked dirty so newer work is not reported as saved.
- When interrupted-save artifacts are detected, review the recovery dialog and its paths before continuing normal work.

## Keyboard Shortcuts

Common operations are available without leaving the canvas.

- Ctrl+N creates a layout, Ctrl+O opens a database, Ctrl+S saves, Ctrl+Z undoes, Ctrl+Y redoes, and Delete removes a selection.
- Ctrl+C copies, Ctrl+X cuts, Ctrl+V starts interactive Paste, Ctrl+Shift+V uses Paste in Place, and Ctrl+B duplicates selected direct objects.
- F or F2 fits the view, Shift+F2 fits the selection, F3 toggles Tool Options, and Ctrl+G opens Go to Position.
- Ctrl+D descends, D opens child selection, Ctrl+A ascends, Escape cancels a tool, and arrow keys navigate or move a selection.
- Q opens Properties for the canvas selection, selected ruler, or active Cells-panel cell.

## Troubleshooting

Use the status bar and a few display checks to diagnose common viewing problems.

- If geometry is missing, check the active cell, layer visibility, hierarchy depth, wireframe setting, and text visibility.
- If selection fails, confirm Select mode is active. Selection targets direct objects or instances in the active cell, not flattened descendant geometry.
- If a drawing options window was hidden with Done, press F3 or use View > Tool Options to restore it.
- For large files, allow Dynamic Layer Rendering to finish progressive layers before judging visual completeness.

## Release Scope & Safe Workflow

Use the Early Access release for focused GDSII review and basic editing, with an external signoff flow.

- Supported workflows include hierarchical GDSII viewing, layers, search, measurement, Properties, basic geometry and instance editing, undo/redo, native project saving, and GDSII export.
- Do not use this application as evidence of DRC, LVS, ERC, antenna, foundry-rule, or tape-out signoff. PCells, OASIS, LEF/DEF, foundry technology decks, and KLayout-compatible scripting are not supported.
- Keep the source GDS unchanged. Import it, save working edits to a separate native OA-like project, and export each review candidate to a new GDS file.
- Reopen the exported GDS and verify the expected top cell, hierarchy, layers, object counts, edited regions, labels, paths, and instance transformations.
- Archive the original GDS, native project, exported GDS, application version, and relevant logs together. Complete foundry-qualified verification in established EDA tools before fabrication.

## Quick reference

Use Ctrl+F in your browser to find a command. Arrow keys navigate when nothing is selected and move selected objects in Edit mode.

- Fit view: F or F2. Fit selection: Shift+F2. Tool Options: F3. Properties: Q.
- Descend: Ctrl+D. Choose child: D. Ascend: Ctrl+A (this is not Select All).
- Undo: Ctrl+Z. Redo: Ctrl+Y. Copy: Ctrl+C. Cut: Ctrl+X. Paste: Ctrl+V. Paste in Place: Ctrl+Shift+V. Duplicate: Ctrl+B.
- Middle-button or secondary-button drag pans the canvas. Select mode click selects one direct object; drag makes a crossing selection. Shift adds; Ctrl removes.
- Done hides Tool Options while keeping the tool active; Cancel returns to Select.
- CACHED and PROGRESSIVE are rendering status labels. Wait for progressive layers to finish before judging completeness.
- Trace Net provides an inspection overlay, not electrical verification or signoff.

## Report a problem

Use the Support and Security documents in the public repository.

- Include Help > About version, operating system, exact steps, expected result, and observed behavior. Include relevant logs when available.
- Never disclose proprietary layouts without authorization. A small non-confidential reproduction is preferable.
- For missing geometry, check active cell, layer visibility, hierarchy detail, text visibility, and progressive completion. Press F to fit.
- For save recovery, inspect the paths reported by the recovery dialog and preserve the original and recovery files before deciding which copy to use.

## Screenshot credits

Example layout: UoM eFPGA from the FPGA-Research eFPGA: RTL-to-GDS with SKY130 project, published upstream under Apache 2.0. Screenshots rendered using Layout AI Agent by SynerRaise; no endorsement by upstream contributors is implied.

[Layout source](https://github.com/FPGA-Research/eFPGA---RTL-to-GDS-with-SKY130) · [License copy](licenses/eFPGA-Apache-2.0.txt). Screenshots illustrate an Early Access interface; appearance may differ by build. Images are embedded in the HTML edition for offline viewing.
