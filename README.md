# ImPlot.jl
Plotting extension library that can be used in conjunction with 
[CImGui.jl](https://github.com/Gnimuc/CImGui.jl) to provide enhanced immediate-mode data 
visualization.

ImPlot.jl provides an interface to [cimplot](https://github.com/cimgui/cimplot), 
which is an auto-generated C API to [implot](https://github.com/epezent/implot), a C++ 
plotting extension library for [imgui](https://github.com/ocornut/imgui).

## Installation

Simple installation via the package registry:

```julia
]add ImPlot
```

NOTE: The current stable version of **ImPlot on the registry is backed by binaries built from implot v0.4**. If you would like to try out some of the newer plot types and features, the development branch is currently running with binaries built from implot v0.8. To use that instead, install via:

```
]add https://github.com/wsphillips/ImPlot.jl#master
```
Also note, there are currently no convenience functions for the newer implot features on the development branch. You will have to work with the lower-level function wrappers in the `LibCImPlot` submodule

## Example Usage

Use `demo/demo.jl` to check if things are working + the demo window that shows off what the 
API can do.

Plots are delcarative and follow a similar pattern as CImGui.jl:

```julia

## within a CImGui.jl render loop
## This assumes you have CImGui.LibCImGui.ImGuiCond_Once in scope
...

if show_window
    @c CImGui.Begin("Plot Window", &show_window)
    y = rand(1000)
    ImPlot.SetNextPlotLimits(0.0,1000,0.0,1.0, ImGuiCond_Once)
    if (ImPlot.BeginPlot("Foo", "x1", "y1", CImGui.ImVec2(-1,300)))
        ImPlot.PlotLine(y)
        ImPlot.EndPlot()
    end
    CImGui.End()
end
```

For some basic Julia imlementation examples, see also `demo/example_plots.jl` Another good
place to look is the [C++ demo
sources](https://github.com/epezent/implot/blob/v0.3/implot_demo.cpp)
