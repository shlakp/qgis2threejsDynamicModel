Exporter
========

.. note:: Now being updated for Qgis2threejs version 2.0.

.. contents:: Contents
   :local:

.. image:: ./images/exporter1.png

General Scene Settings
----------------------

World Settings
~~~~~~~~~~~~~~

Menu ``Scene - World Settings...``
.. image:: ./images/world_settings.png

* Base size

   Size in 3D world that corresponds to the map canvas width. The
   default value is 100.

* Vertical exaggeration

   Vertical exaggeration factor. This value affects terrain shape and z
   positions of all vector 3D objects. This also affects 3D object height
   of some object types with volume. Object types to be affected:

    | Point : Cylinder, Cube, Cone
    | Polygon : Extruded

   3D objects of the following types have volume, but their heights aren't
   affected by this factor:

    | Point : Sphere, JSON model, COLLADA model
    | Line : Pipe, Cone, Box

   The default value is 1.5.

* Vertical shift

   Vertical shift for all objects. If you want to export high altitude
   and narrow area, you should adjust the object positions to be
   displayed at the center of browser by changing this value. If you set
   the value to -1000, all objects are shifted down by 1000 in the unit of
   map CRS.

* Background

   Select either sky-like gradient or a solid color for the background of
   scene. Default is Sky.

* Display of coordinates

   If the ``Latitude and longitude (WGS84)`` option is selected,
   coordinates of clicked position on a 3D object are displayed in
   longitude and latitude (WGS84). If
   `Proj4js <https://github.com/proj4js/proj4js>`__ doesn't support current
   map CRS, this option is disabled.

Controls
~~~~~~~~

Menu ``Scene - Controls``

`OrbitControls <https://raw.githubusercontent.com/minorua/Qgis2threejs/master/js/threejs/controls/OrbitControls.txt>`__ is available.


DEM Layer Settings
------------------

Geometry
^^^^^^^^

* Resampling level

   Select a DEM resolution from several levels. This resolution is used to
   resample the DEM, but is not for texture.

* Surroundings

   This option enlarges output DEM by placing DEM blocks around the main block of the map canvas extent.
   Size can be selected from odd numbers in the range of 3 to 9. If you select 3, total 9 (=3x3) blocks
   (a center block and 8 surrounding blocks) are output. Roughening can be selected from powers of 2 in
   the range of 1 to 64. If you select 2, grid point spacing is doubled. It means that the number of
   grid points in the same area becomes 1/4.

* Clip DEM with polygon layer

   Clips the DEM with a polygon layer. If you have a polygon layer that
   represents the area that elevation data exist or represents drainage basins,
   you might want to use this option.


Material
^^^^^^^^

* Display type

   You can choose from map canvas image, layer image, a image file or a
   solid color.

   * Map canvas image

      Render a texture image with the current map settings for each DEM block.

   * Layer image

      Render a texture image with the selected layer(s) for each DEM block.

   * Image file

      Textures the main DEM block with existing image file such as PNG file and JPEG file.
      TIFF is not supported by some browser. See `Image format
      support <http://en.wikipedia.org/wiki/Comparison_of_web_browsers#Image_format_support>`__
      for details.

   * Solid color

      To select a color, press the button on the right side.

* Resolution

   Increases the size of image applied to each DEM block. This option is enabled when
   either ``Map canvas image`` or ``Layer image`` is selected. You can select a ratio
   to map canvas size from 100, 200 and 400 (%). Image size in pixels follows the percent.

* Opaciy

   Sets opacity of the DEM. 100 is opaque, and 0 is transparent.

* Transparent background (With map canvas image or layer image)

   Makes background of the image to be rendered transparent.

* Enable transparency (With image file)

   Enables the image transparency.

* Enable shading

   Adds a shading effect to the DEM.


Other Options
^^^^^^^^^^^^^

* Build sides

   This option adds sides and bottom to each DEM block. The z position of bottom
   in the 3D world is fixed. You can adjust the height of sides by changing
   the value of vertical shift option in the World panel. If you want to
   change color, edit the output JS file directly.

* Build frame

   This option adds frame to the DEM. If you want to change color, edit the output
   JS file directly.


Vector Layer Settings
---------------------

Vector layers are grouped into three types: Point, Line and Polygon.
Common settings for all types:

* Z coordinate

    Specifies object altitude above zero-level or a DEM surface.

    * Altitude

        You can use a expression to specify altitude. The unit is that of the map CRS.
        When Z value or M value is selected, the evaluated value is added to it.

        * Z value
        This item can be selected when the layer geometries have z coordinates and
        the layer type is point or line.

        * M value
        This item can be selected when the layer geometries have m values and
        the layer type is point or line.

    * Altitude Mode

        * Absolute
        Altitude is distance above zero-level.

        * Relative to DEM layer
        Altitude is distance above a DEM surface.

* Style

   Usually, there are options to set object color and transparency. Refer
   to the links below for each object type specific settings. The unit of
   value for object size is that of the map CRS.

* Feature

   Select the features to be output.

    * All features

      All features of the layer are exported.

    * Features that intersect with map canvas extent

      Features on the map canvas are exported.

        * Clip geometries

          This option is available with Line/Polygon layer. If checked, geometries are clipped by the extent of map canvas.

* Attribute and label

   If the export attributes option is checked, attributes are exported with
   feature geometries. Attributes are displayed when you click an object on
   web browser.

   If a field is selected in the label combobox, a label is displayed above
   each object and is connected to the object with a line. This combo box
   is not available when layer type is line.

Point
^^^^^

Point layers in the project are listed as the child items. The following
object types are available:

    Sphere, Cylinder, Cone, Box, Disk

See :ref:`object-types-point-layer` section in :doc:`ObjectTypes` page for each object type specific settings.

Line
^^^^

Line layers in the project are listed as the child items. The following
object types are available:

    Line, Pipe, Cone, Box, Profile

See :ref:`object-types-line-layer` section in :doc:`ObjectTypes` page for each object type specific settings.

Polygon
^^^^^^^

Polygon layers in the project are listed as the child items. The
following object types are available:

    Extruded, Overlay

See :ref:`object-types-polygon-layer` section in :doc:`ObjectTypes` page for each object type specific settings.


Menu
----
* File
    * Export to Web
        現在のシーンをWebブラウザで表示するためのファイルを出力します。
        See `Export to Web Dialog <#exporttowebdialog>`__ section.

    * Save Scene As - Image (.png)
        現在のシーンを画像に保存します。

    * Save Scene As - glTF (.gltf,.glb)
        現在のシーンをglTF形式で保存します。

    * Plugin Settings...
        プラグインの設定ダイアログを開きます。

    * Close Exporter
        エクスポータを閉じます。

* Scene

    * World Settings...
        ワールド設定ダイアログを開きます。

    * Camera
        * Perspective
            近くのものは大きく、遠くのものは小さく見えるように表示します

        * Orthographic

    * Controls - Orbit

    * Clear All Settings
        現在のエクスポート設定をクリアします。

    * Reload (F5)
        ページを再読込します。

    * Reset Camera Position (Shift+R)
        カメラの位置と向きを初期状態に戻します。

* Window
    * Panels
        * Layers
            現在のプロジェクトに含まれるレイヤが表示されます。

        * Console
            コンソールにはデバッグのための情報が表示されます。主にJavaScript側のデバッグ情報が表示されます。
            Python側のデバッグ情報はQGISメインウィンドウのログに表示されます。
            JavaScriptのステートメントを入力して実行することもできます。

    * Always on Top
        ウィンドウを最前面に表示します。

* Help
    * Help
        ドキュメントをウェブブラウザで開きます。インターネット接続が必要です。

    * Plugin Homepage
        プラグインのホームページをウェブブラウザで開きます。インターネット接続が必要です。

    * Send feedback
        プラグインのバグトラッカーをウェブブラウザで開きます。インターネット接続が必要です。

    * About Qgis2threejs Plugin
        プラグインのバージョンを表示します。

Export to Web Dialog
--------------------

.. image:: ./images/export_web.png

* Combo box to select a template

   Select a template from available templates:

    * 3DViewer

       This template is a 3D viewer without any additional UI library.

    * 3DViewer(dat-gui)

       This template has a `dat-gui <https://code.google.com/p/dat-gui/>`__
       panel, which makes it possible to toggle layer visibility, adjust layer
       opacity and add a horizontal plane movable in the vertical direction.

* Output directory and HTML Filename

   Select output HTML file path. Usually, a js file with the same file
   title that contains whole data of geometries and images is output into
   the same directory, and some JavaScript library files are copied
   into the directory. Leave this empty to output into temporary
   directory. Temporary files are removed when you close the QGIS
   application.

* Export button

   Exporting starts when you press the Run button. When the exporting has
   been done, the exported page will be opened in web browser. At this
   time, export settings are automatically saved to a file under the same
   directory as the project file if you are working with a project file.
   Later the export settings of the project will be automatically loaded
   into the plugin.

   Pressing the Help button will open the local document with default web
   browser.


Exporter Settings
-----------------

.. image:: ./images/plugin_settings.png

* Browser path

   If you want to open web page exported from the exporter with a web browser
   other than the default browser, enter the web browser path in this input box.
   See `Browser Support <https://github.com/minorua/Qgis2threejs/wiki/Browser-Support>`__ page.


* Optional Features

   Not available in version 2.0 yet.
