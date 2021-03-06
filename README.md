## Code for L1 Path Smoothing for Video Optimization

| file | description |
| --- | --- |
| `videostab.cpp[h]` | the main function for running L1 path smoothing |
| `stablization_test.cpp` | runs videostab |
| `videostablization.pro`| Qt project files |
| `common.pri`, `libstablization.pro`,`stablization_test.pro` | more Qt project files |

Dependency: lp-solve, opencv3.0, cvplot (has been copy-paste into videostab.cpp[h] so no need for extenral lib)

Using lp-solve:

1. download from http://lpsolve.sourceforge.net/5.5/
 
2. unzip and cd to the folder (suppose it is lp_solve_5.5/ )

3. cd lpsolve55
    sh ccc  (and you should see folder bin/ux64/)

4. include the library in the project
    in qt, change the following lines in libstablization.pro to actual lp_solve_5.5 path

    LIBS += -L"/home/memgrapher/Code/lp_solve_5.5/lpsolve55/bin/ux64/" -llpsolve55
    
    INCLUDEPATH += /home/memgrapher/Code/lp_solve_5.5
    
    DEPENDPATH  += /home/memgrapher/Code/lp_solve_5.5
    
## Code for L2 video smoothing,face saliency constraint and face decoration

| file | description |
| --- | --- |
| `VideoStablization.cpp[h,vcxproj]` | the main functions |
| `CMakeLists.txt` | cmake |
| `cvplot`  | lib files for cvplot, used for plotting trajectory |

Dependency: OpenFace, opencv3.0, cvplot

download OpenFace from https://github.com/TadasBaltrusaitis/OpenFace and follow instruction.

## Result files

| file | description |
| --- | --- |
| `video-stabilization-face.pdf` | report. including links to Youtube video of algorithm output |
| `L1-X.png`, `L1-Y.png`, `L1-Angle.png` | L1-optimized path from running videostab on SANY0025.avi. Note to TA and Instructor: the figure in our report submitted on Gradescope is incorrect. These are the correct version |

## Data files (in data folder
| file | description |
| --- | --- |
| `SANY0025.avi`, `gleicher1.mp4`, `gleicher2.mp4`,`new_gleicher.mp4` | example shaky video. obtained from http://www.cc.gatech.edu/cpl/projects/videostabilization/. |
|`SANY0025_warp.avi`,`new_gleicher_warp.avi`| output of our L1 path smoothing algorithm |

## L1 path smoothing (videostab.cpp) usage

put videostab.cpp[h] and stablization_test.cpp in videostab/, and import videostab.pro into Qt. Change input and output file path in stablization_test.cpp.

lp-solver run time is 6s for 330 frames, 12s for 450 frames.

## VideoStablization (L2, face salient constraint, face decoration) usage

in build folder, run make, and then

    ./bin/VideoStablization -f [input file] [-salient 0.9] [-crop 0.1] [-pathsmooth 20] [-facesmooth 5]
    
default value: 

sallient = 0 //not use face feature

hcrop =0.1 //crop 10% of wide and height on both edge

pathsmooth=20 //radius for smoothing trajectory.

facesmooth=5 //radius for smoothing face feature to center

