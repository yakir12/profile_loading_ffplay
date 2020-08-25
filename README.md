Follow these steps to build `ffmpeg` with/out `ffplay` and then profile the loading times.

# Instructions
1. build `FFMPEG_jll` with `ffplay`:
   ```
   ~$ env BINARYBUILDER_AUTOMATIC_APPLE=true julia --color=yes build_tarballs.jl --debug --verbose --deploy="yakir12/FFMPEG_jll.jl"
   ```
   (you might need to first delete `https://github.com/yakir12/FFMPEG_jll.jl`)
2. test vanila `ffmpeg`:
   ```julia
   import Pkg
   path = mktempdir()
   cd(path)
   Pkg.activate(path)
   Pkg.add.(["BenchmarkTools", "FFMPEG_jll"])
   using FFMPEG_jll, BenchmarkTools
   @btime run(`julia --project=. -e "using FFMPEG_jll"`)
   ```
3. test `ffplay` `ffmpeg` (in a separate julia session):
   ```julia
   import Pkg
   path = mktempdir()
   cd(path)
   Pkg.activate(path)
   Pkg.add(url = "https://github.com/yakir12/FFMPEG_jll.jl")
   Pkg.add("BenchmarkTools")
   using FFMPEG_jll, BenchmarkTools
   @btime run(`julia --project=. -e "using FFMPEG_jll"`)
   ```

# Results

On my Linux (Debian) machine I get these times:
```


