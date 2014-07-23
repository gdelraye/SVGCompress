===========
SVGCompress
===========
---------------
Highlights
---------------

SVGcompress is a pure python module for simplifying/compressing svg (Scalable Vector Graphics) files. Have you ever tried to output a plot in vector format (pdf, svg, eps, etc.) and been surprised that your file weighs 10 or 20MB? Needed to submit a vector figure for publication but run up against the file size limit? Before you try to get away with the old standby of embedding a raster image in your vector and hoping the journal doesn’t notice, try SVGCompress! SVGCompress can help pare down your file size by:

     * Removing tiny polygons - Reduce the number of polygons in your image by removing those below a small threshold size. The size threshold can be based on polygon area or circumference.

     * Simplifying shapes - Reduce the complexity of your polygons using the Ramer–Douglas–Peucker algorithm.

     * Merging adjacent or overlapping shapes - Merging can be accomplished by taking the union of overlapping polygons or through the construction of a minimum convex hull.

----------------
Installation
----------------
SVGCompress has only been tested in Python 2.x

Installation should be through pip (pip install SVGCompress)

Requires the following non-standard libraries:

     * Numpy; svg.path; Shapely; rdp

*Important*
===========
SVGCompress depends upon Shapely, which requires the GEOS framework (http://trac.osgeo.org/geos). If you operate on Windows, pip will install the required files along with Shapely, but this will NOT happen with other operating systems. For non-Windows users, the most convenient way of installing the GEOS framework is through a program such as Canopy (free with academic license) or similar IDLE with an included package manager.

----------------
Usage Notes
----------------
Usage of SVGCompress is through the class Compress, or through the convenience function compress_by_method. The function svg_compress.test() contains usage examples demonstrating all of the compression methods with compress_by_method.

Producing your figures in svg format can be done through Matplotlib. This is especially convenient if you have a graphics editor such as Inkscape (free) which will allow you to do things such as modify the font and color of text or lines directly in the svg, without having to re-run your code. You can also use this to convert one of your svg files into an alternate vector format such as pdf or eps.

--------------
Examples
--------------
SVGCompress/test contains examples of each compression algorithm on three different files: One is a demonstration graphic (test_vector.svg) and the second and third are actual vector plots (map_test.svg, matplotlib_test.svg)

For example, running the following call to SVGCompress.compress_by_method::

	compress_by_method(filename, 'merge', curve_fidelity, outputfile, pre_select = True, 
			   selection_tuple = (criterias[0], thresholds[0]), epsilon = epsilon, 
			   bufferDistance = buffer_distance, operation_key = 'hull')

compresses the test_vector.svg demonstration file from 87 to 30 KB by constructing convex hulls (operation_key = 'hull') around small neighboring polygons (bounding box area < 1000 pixels) to lessen the total number of polygons and then using the Ramer–Douglas–Peucker algorithm to simplify them. The 'test_vector series' in the folder 'test' contains examples of other compression routines. Note that these examples were designed to make the changes that occur during compression obvious. For a more subtle example of compression, see the map_test series.

--------------
Version
--------------
0.19 - Not extensively tested. Please email me to let me know of any issues.

Changelog
============
**0.19 (JULY/22/2014)**

        * Changed compress_by_merging default behavior to group_by_color = True

        * Appended README with critical information on Shapely installation

**0.18 (JULY/22/2014)**

	* Fixed issue with clipping paths - Code previously threw an exception when trying to extract coordinate data from clipping paths

	* Updated README with a usage example

	* Fixed bug in install_requires that crashed installation with pip
