# How to plot FreeFem++ Simulations in Matlab and Octave

Once you have successfully simulated a PDE problem using FreeFem++ you may want to have a look at your simulation results from within Matlab&copy; or Octave. In this repository you will find some code snippets showing how to make this wish come true.

## Basic Theory

The purpose of a FE mesh is to describe a spatial geometry - for example a CAD object. A FE mesh is built from mesh elements. Mesh elements have the shape of a triangle or rectangle, can vary in size and the nodes (vertices) are not necessarily bound to a rectangular grid. If we look at a meshed object the surface may be colored according to the solution of a PDE which - for the sake of simplicity - shall be given at the mesh nodes only. Finally parts of the FE mesh may be obscured depending on the point of view.<br>
At the other hand the `patch()` command which is built into Matlab&copy; and Octave renders a set of polygons (=facets, patches). The patch drawing primitives are defined by a color value and the spatial coordinates at the polygon vertices. We can associate these drawing primitives with FE mesh elements and looking towards a plot implementation all the prerequisites stated will be met.<br>
In the current implementation the mesh data (i.e. the PDE solution at the mesh nodes and the nodal coordinates) has to be written to a text file via the FreeFem++ script. In order to plot the problem with the `patch()` command this file must be parsed and processed by the `ffmatlib` library. Basically, the `ffmatlib` library splits and rearranges the continuous vertice data because `patch()` expects its input data to be clustered patch-wise. A detailed documentation of the `patch()` command can be found at [1](https://de.mathworks.com/help/matlab/ref/patch.html), [2](https://de.mathworks.com/help/matlab/visualize/introduction-to-patch-objects.html) and [3](https://de.mathworks.com/help/matlab/creating_plots/how-patch-data-relates-to-a-colormap.html).

![](https://raw.githubusercontent.com/samplemaker/freefem_matlab_octave_plot/public/screenshots/3dsurf_10.png)

## Source Code Snippets

### Getting started

Two minimum examples:

  * Run
    * FreeFem++ `demo1_getstarted.edp`
    * From within Matlab/Octave run `demo1_getstarted1.m`
    * From within Matlab/Octave run `demo1_getstarted2.m`

[Screenshot: minimum example](https://raw.githubusercontent.com/samplemaker/freefem_matlab_octave_plot/public/screenshots/2dgetstarted1.png)  
[Screenshot: minimum example](https://raw.githubusercontent.com/samplemaker/freefem_matlab_octave_plot/public/screenshots/2dgetstarted2.png)  

### Creating 2D Plots

The 2D plot examples focus on displaying functions of the type R<sup>2</sup> &rarr; R or 2D meshes:

  * Run
    * FreeFem++ `demo2_plot2d.edp`
    * From within Matlab/Octave run `demo2_plot2d.m`

[Screenshot: density plot](https://raw.githubusercontent.com/samplemaker/freefem_matlab_octave_plot/public/screenshots/2ddensity.png)  
[Screenshot: surf plot](https://raw.githubusercontent.com/samplemaker/freefem_matlab_octave_plot/public/screenshots/2dsurf.png)  
[Screenshot: 2D-mesh](https://raw.githubusercontent.com/samplemaker/freefem_matlab_octave_plot/public/screenshots/2dmesh.png)  

### Creating 3D Plots

The 3D plot examples focus on displaying functions of the type R<sup>3</sup> &rarr; R (i.e. a 3D object boundary colored with a scalar value like a temperature) or 3D mesh surfaces:

  * Run
    * FreeFem++ `demo3_plot3d_cyl.edp`
    * FreeFem++ `demo3_plot3d_box.edp`
    * From within Matlab/Octave run `demo3_plot3dbd.m`

[Screenshot: surf plot](https://raw.githubusercontent.com/samplemaker/freefem_matlab_octave_plot/public/screenshots/3dsurf_2.png)  
[Screenshot: surface of a 3D-mesh](https://raw.githubusercontent.com/samplemaker/freefem_matlab_octave_plot/public/screenshots/3dmesh.png)

### Advanced: Cutting 3D Simulations

To make the inside visible it is also possible to cut a 3D FreeFem++ simulation along a slicing plane. You have to write the mesh elements as well as the boundary information to use this feature:

  * Run
    * From within Matlab/Octave run `demo4_start_slicer_gui.m`
    * A minimum example: `demo4_slice3d.m`

[Screenshot: slice3d](https://raw.githubusercontent.com/samplemaker/freefem_matlab_octave_plot/public/screenshots/3dsurf_slice7.png)  
[Screenshot: boundary](https://raw.githubusercontent.com/samplemaker/freefem_matlab_octave_plot/public/screenshots/3dsurf_slice8.png)  
[Screenshot: cross section](https://raw.githubusercontent.com/samplemaker/freefem_matlab_octave_plot/public/screenshots/3dsurf_slice9.png)  
[Screenshot: GUI-Slicer](https://raw.githubusercontent.com/samplemaker/freefem_matlab_octave_plot/public/screenshots/GUI_Slicer.png)  

### Advanced: 2D Contour

For 2D problems it is sometimes helpful to have an isovalue - plot which will be created in the following example:<br>

  * Run
    * FreeFem++ `demo5_isovalues_2d.edp`
    * From within Matlab/Octave run `demo5_isovalues_2d.edp`

[Screenshot: isovalues](https://raw.githubusercontent.com/samplemaker/freefem_matlab_octave_plot/public/screenshots/2dsurf_isovalues.png)  
[Screenshot: surf](https://raw.githubusercontent.com/samplemaker/freefem_matlab_octave_plot/public/screenshots/2dsurf_surf.png)  

### Advanced: 2D Vector Fields

For 2D problems it is sometimes helpful to have an vector field - plot as well. Such a plot  will be created in the following example:<br>

  * Run
    * FreeFem++ `demo6_vector_2d.edp`
    * From within Matlab/Octave run `demo6_vector_2d.m`

[Screenshot: vectorfields](https://raw.githubusercontent.com/samplemaker/freefem_matlab_octave_plot/public/screenshots/2dvectorfield.png)  

### Advanced: Interpolation of a 3D Mesh on a Rectangular Grid

  * Run
    * FreeFem++ `demo7_slice3d.edp`
    * Build MEX - File `./ffmatlib/fftet2gridfast.c`
    * From within Matlab/Octave run `demo7_slice3d_2dgrid.m`

[Screenshot: plane definition](https://raw.githubusercontent.com/samplemaker/freefem_matlab_octave_plot/public/screenshots/3dplanedefinition.png)  
[Screenshot: 3D cross section interpolation](https://raw.githubusercontent.com/samplemaker/freefem_matlab_octave_plot/public/screenshots/3dinterpolation.png)  
[Screenshot: 3D cross section projection](https://raw.githubusercontent.com/samplemaker/freefem_matlab_octave_plot/public/screenshots/3dcrossprojection.png)  

### Advanced: 3D Vector Fields on Cross Sections

  * Run
    * FreeFem++ `demo8_slice3d_vectors.edp`
    * Build MEX - File `./ffmatlib/fftet2gridfast.c`
    * From within Matlab/Octave run `demo8_slice3d_2dgrid_vectors.m`

[Screenshot: 3D cross section vector field](https://raw.githubusercontent.com/samplemaker/freefem_matlab_octave_plot/public/screenshots/3dvectorfield.png)  

## Implementation - FreeFem++

Hint: The `patch()` command draws and colors flat facets based on the coordinates and color values given on each vertex. If a higher order FE-space (e.g. P2 elements) was choosen the PDE solution can have a higher degree of freedom as can be visualized.

### 2D Problems

From within the FreeFem++ script write the mesh elements (triangles defined by its vertices) and the solution of the PDE at the nodes respectively:

```Matlab
ofstream tridata ("export_tri.txt");
for (int i=0; i<Th.nt; i++){
  for (int j=0; j<3; j++){
    tridata << Th[i][j].x << ";"
            << Th[i][j].y << ";"
            << u[][Vh(i,j)] << "\n";
  }
}
```

### 3D Boundary Value Problems

If the domain boundary (surface) is to be displayed it is enough to write the boundary elements only:

```Matlab
int idx;
int nbelement=Th3d.nbe;
ofstream bddata ("boundary_file.txt");
for (int k=0;k<nbelement;++k){
  for (int num=0;num<3;num++){
    idx=Th3d.be(k)[num];
    bddata << Th3d(idx).x << ";"
           << Th3d(idx).y << ";"
           << Th3d(idx).z << ";"
           <<  u(Th3d(idx).x,Th3d(idx).y,Th3d(idx).z) << "\n";
  }
}
```

### Advanced: Cutting 3D Problems
If a cross section is to be made it is necessary to write the mesh elements (tetrahedra) as well as the boundary data:

```Matlab
ofstream tetdata ("export_tet.txt");
for (int i=0; i<Th3d.nt; i++){
  for (int j=0; j<4; j++){
    tetdata << Th3d[i][j].x << ";"
            << Th3d[i][j].y << ";"
            << Th3d[i][j].z << ";"
            << u[][Vh(i,j)] << "\n";
  }
}
```

### Advanced: 2D Vector Fields

In order to plot 2D vector fields just write multiple columns:

```Matlab
ofstream file ("export_tri_ncols.txt");
for (int i = 0; i < Th.nt; i++){
  for (int j = 0; j < 3; j++){
    file << Th[i][j].x << ";"
         << Th[i][j].y << ";"
         << uh[][Vh(i,j)] << ";"
         << vh[][Vh(i,j)] << "\n";
  }
}
```

## Implementation - Matlab&copy;/Octave

Hint: The library functions can be found in the folder `ffmatlib`. Use the `addpath(path to ffmatlib)` command if you are working in a different directory.

### General plotting in 2D and 3D Boundary Value Plots

The function `ffread2patch()` reads a file and rearranges its content in such a way that diagrams can be created with the `patch()` command. It's arguments depend on the number of columns and on the separation character. `ffread2patch()` can process 2D mesh elements or 3D boundary data (triangles):

```Matlab
[X,Y,C, ...] = ffread2patch('filename.txt','Delimiter',';','Format','auto');
```
The number of columns can be set explicitly via the format identifier:

```Matlab
[X,Y,Z,C] = ffread2patch('filename.txt','Delimiter',';','Format','%f %f %f %f');
```
X, Y and C are matrices which can be supplied to `patch()`.

Hint: You can split the reading and conversion process into two different entities:

```Matlab
[tridata] = ffreadfile('File1','filename.txt','Delimiter',';','Format','%f %f %f');
[X,Y,C] = fftri2patch(tridata);
```

### Advanced: Cutting 3D Problems

To make a cut from a 3D problem, both the edge data and the mesh element data must be loaded. This can be achieved with the following function call:

```Matlab
[file1data,file2data] = ffreadfile ('File1','filename1.txt','File2','filename2.txt', ...
                                    'Delimiter',';','Format','%f %f %f %f')');
```

The cut is executed with the following two commands:

```Matlab
[BX,BY,BZ,BC] = slicebd2patch (boundarydata,S1,S2,S3);
[SX,SY,SZ,SC] = slicetet2patch (meshdata,S1,S2,S3);
```

The input arguments `S1..S3` contain x,y,z coordinates of three points defining the slicing plane. The output data `(BX,BY,BZ,BC)` and `(SX,SY,SZ,SC)` or the superposition of both `([SX BX],[SY BY],[SZ BZ],[SC BC])` can be plot with the `patch()` command.

Note: The intersection [SX,SY,SZ,SC] which is consisting of a subset of tetrahedrons can be interpolated onto a rectangular grid (smoothing the cross section). The method used is a Barycentric Coordinate interpolation. To speed up the interpolation the interpolation routine is implemented in MEX and must be compiled before usage. You may have a look at the section "Notes on Compilation".

```Matlab
[C] = fftet2gridfast(meshdata,X,Y,Z);
```
where meshdata contains the tetrahedron vertex coordinates and a scalar for all tetrahedron vertices. X, Y, Z defines a rectangular grid in 3d to which the scalar value is to be interpolated.

### Advanced: Slicer_GUI

There's a graphical user interface (working in both worlds, Matlab and Octave) that makes it easier to create cross-sections of PDE problems. The function call is:

```Matlab
slicer_gui(bddatafile,tetdatafile);
```
You may also have a look at `demo4_start_slicer_gui.m`.

### Advanced: 2D Contour

To create iso-level curve plots with the Matlab / Octave `contour ()` command, the data must be interpolated on a rectangular grid. In a first step load the raw data:

```Matlab
[tridata] = ffreadfile('File1','filename.txt','Delimiter',';','Format','%f %f %f');
```

Then interpolate the third column in `tridata` on a rectangular grid defined by X and Y. If grid points are outside from any triangles the function will return NaN's.

```Matlab
C = fftri2grid(tridata,X,Y);
```

The result can be plot with the command:

```Matlab
[c,h] = contour(X,Y,C,8);
```

Note: There is a one to one replacement MEX implementation available for `fftri2grid.m` which can be considered to be approx. x33 faster. See `./ffmatlib/fftri2gridfast.c` and the section "Notes on Compilation" for more informations.

### Advanced: 2D Vector Fields

To create vector field plots with the Matlab / Octave command `quiver()` it is necessary to interpolate the data given on the mesh vertices on a rectangular grid. In a first step load the raw data:

```Matlab
[tridata] = ffreadfile('File1','filename.txt','Delimiter',';','Format','%f %f %f');
```

Then interpolate the data columns in `tridata` on a rectangular grid defined by X and Y. If grid points are outside from triangles the function will return NaN's.

```Matlab
[U,V] = fftri2grid(tridata,X,Y);
```

The result can be plot with the command:

```Matlab
quiver(X,Y,U,V);
```

Note: There is a one to one replacement MEX implementation available for `fftri2grid.m` which can be considered to be approx. x33 faster. See `./ffmatlib/fftri2gridfast.c` for more informations.

### Advanced: 3D Vector Fields and Cross Section Interpolation

The function `fftet2gridfast()` is able to create cross sections of higher order vector fields as well. Multiple columns in `meshdata` can be written and the function can be simply called via:

```Matlab
[V1,V2, ...] = fftet2gridfast(meshdata,X,Y,Z);
```
For more information see section "Cutting 3D Problems".

### Notes on Compilation

Octave:

In Octave seek to the folder `./ffmatlib/` and invoke the command `mkoctfile --mex -Wall fftet2gridfast.c`.

Windows:

Under Windows with Microsoft Visual Studio invoke `mex fftet2gridfast.c -v -largeArrayDims COMPFLAGS='$COMPFLAGS /Wall'`. It is to mention that C99 standart must be used and which must be configured in advance. If your build fails with Microsoft Visual Studio 10 you can try to change the filename into *.cpp which forces MVSD to use a c++ compiler.

## Files

  * `ffread2patch.m` Reads FreeFem++ simulation results and converts the vertex/triangle data into patch plot data.
  * `ffreadfile.m` Reads one or two FreeFem++ simulation result files.
  * `fftri2patch.m` Converts vertex/triangle data into patch plot data.
  * `slicetet2patch.m` Cuts 3D mesh elements (tetrahedrons) and converts the cross section into patch plot data.
  * `fftet2gridfast.c` Interpolates from 3d tetrahedral mesh to a rectangular grid.
  * `slicebd2patch.m` Cuts the boundary data and converts remaining rest into patch plot data.
  * `demo4_start_slicer_gui.m` Starts the slicer graphical user interface (Slicer_GUI) to cut 3D data.
  * `slicer_gui.m` Graphical user interface for cuttig FreeFem++ simulations.
  * `fftri2grid.m` Interpolates from 2D triangular mesh to 2D rectangular grid.
  * `fftri2gridfast.c` Replacement for `fftri2grid.m` which is approx. x33 faster.

## Software

  * [FreeFem++][freefem]
  * [Octave][octave]
  * [Matlab][matlab]

[freefem]:    http://www.freefem.org/
             "FreeFem++ solver for partial differential equations"
[octave]:     https://www.gnu.org/software/octave/
             "GNU Octave scientific programming language"
[matlab]:     https://www.mathworks.com/
             "Matlab scientific programming language"

## Hardware Acceleration

It should be emphasized that the responsiveness of the plots is highly dependent on the degree of freedom of the PDE problem and the capabilities of the graphics hardware. For larger problems (lots of thousand of vertices), a dedicated graphics card rather than on board graphics should be preferred. Make use of hardware acceleration extensively. Some notes on trouble shooting and tweaking:<br><br>
 If `get(gcf,'RendererMode')` is set to auto Matlab/Octave will decide on its own which renderer is the best for the current graphic task.

  * `get(figure_handle,'Renderer')` returns the current figure() renderer
  * `set(figure_handle,'Renderer','OpenGL')` forces a figure() to switch to OpenGL
  * `set(figure_handle,'Renderer','painters')` forces a figure() to switch to vector graphics

Generally OpenGL can be considered to be faster than painters. To get an OpenGL info you can type `opengl info` within Matlab. Ensure the line `Software` shows `false` otherwise OpenGL will run in software mode. If hardware-accelerated OpenGL is available on the system, you can manually change the modes using the `opengl software` and `opengl hardware` commands.

## The License

GPLv3+

Have fun ...
