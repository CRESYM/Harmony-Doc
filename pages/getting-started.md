## Installation and Usage

See the [detailed installation instructions](installation.html).

### Prerequisites 
Harmony can be compiled on Windows. The requirements are:
- [Visual Studio](https://visualstudio.microsoft.com) - version 2022 or newer, with a "Desktop Development for C++" workload installed (See [installation docs.](https://learn.microsoft.com/en-us/visualstudio/install/install-visual-studio?view=vs-2022))
- [miniconda](https://www.anaconda.com/docs/getting-started/miniconda/main) - a miniature version of Anaconda that includes only conda, Python, and a few other packages. (You can also use Anaconda if it is already installed on your machine.)
  
> [!WARNING]
> When installing miniconda, make sure you select the option **'Add to path'**. This will allow you to use miniconda from Visual Studio, Git Bash, etc. If you forgot this, have a look at Step 3 in [this blog post](https://eduand-alvarez.medium.com/setting-up-anaconda-on-your-windows-pc-6e39800c1afb), which shows how to add miniconda to your path. Alternatively, you may reinstall miniconda.

- [Gurobi Optimizer](https://www.gurobi.com/downloads/gurobi-software/?_gl=1*nfc3bz*_up*MQ..*_ga*Mzk5NjUzMDE0LjE3NDk3NDM5OTU.*_ga_RTTPP25C8N*czE3NDk3NDM5OTQkbzEkZzEkdDE3NDk3NDQxMTIkajYwJGwwJGgxNzI0MDAwOTc3) - requires a license (free for academics).
- [Matplot++](https://alandefreitas.github.io/matplotplusplus/) - installed through an MSI provided in the GitHub Releases. For example [v1.2.0](https://github.com/alandefreitas/matplotplusplus/releases/tag/v1.2.0).
- [gnuplot](https://sourceforge.net/projects/gnuplot/) - required by Matplot++ at runtime. Install through one of the [provided installers](https://sourceforge.net/projects/gnuplot/files/gnuplot/).

> [!WARNING]
> When installing gnuplot, make sure you select the option **'Add application directory to your PATH environment variable'**. The option can be a bit hidden in the installer so pay close attention. This option allows gnuplot to be discoverable by Harmony at execution time. 

### Build and Run
To build and run Harmony, open Visual Studio and select "Continue without code" on the welcome dialogue. From the top menu, select View->Terminal. This will open the Visual Studio developer prompt. From there, type the following commands:

```bash
# Donwload the repository
git clone https://github.com/CRESYM/Harmony.git
cd Harmony

# Create conda environment with dependencies
conda env create -f environment.yml
conda activate harmony

# Configure the project
mkdir build
cd build
cmake .. -DGUROBI_PATH="gurobi_installation_dir_config" -DMATPLOT_PATH="matplot++_installation_dir"
# e.g. cmake .. -DGUROBI_PATH="C:\gurobi1202\win64" -DMATPLOT_PATH="C:\Program Files\Matplot++ 1.2.0"

# Compile Harmony
cmake --build . --config Release

# Run Harmony
cd Release
./Harmony
```

### Run the tests
To run the tests, you should follow a similar procedure as for the building and running the code.
```bash
# Open the tests directory
cd tests

# Activate the harmony conda environment
conda activate harmony

# Configure the project
mkdir build
cd build
cmake .. -DGUROBI_PATH="gurobi_installation_dir_config" -DMATPLOT_PATH="matplot++_installation_dir"
# e.g. cmake .. -DGUROBI_PATH="C:\gurobi1202\win64" -DMATPLOT_PATH="C:\Program Files\Matplot++ 1.2.0"

# Compile the tests
cmake --build . --config Release

# Run the tests
ctest
```