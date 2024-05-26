# Configuration of Amaya for SMT-COMP
Repository for sumbissions of [Amaya](https://github.com/MichalHe/amaya) to [SMT-COMP](https://smt-comp.github.io/).

I don't know Docker, so it's likely some things are done in a stupid way.  Please correct if you find a better way.
Many things 

## Compilation

### Installing and running the BenchExec Docker image
```bash
$ docker run registry.gitlab.com/sosy-lab/benchmarking/competition-scripts/user:latest
...
$ docker container run --name benchexec -it registry.gitlab.com/sosy-lab/benchmarking/competition-scripts/user
```

### Installing prerequisites

```
cd /home
apt install git cmake gcc make python3 python3-pip libgmp-dev libhwloc-dev pkg-config
```

### Installing Sylvan
```
git clone 'https://github.com/trolando/sylvan.git'
cd sylvan
git checkout v1.5.0
sed -i 's/-Werror//g' CMakeLists.txt  # Temporarily disable treating warnings as errors; allows building with newer GCC
mkdir build
cd build
cmake -DBUILD_SHARED_LIBS=ON ..
make
make test
sudo make install
```

### Compiling Amaya's C++ backend
```bash
git clone https://github.com/MichalHe/amaya-mtbdd.git
cd amaya-mtbdd
make shared-lib
AMAYA_MTBDD_DIR="$(pwd)"
```

### Installing Amaya's python dependencies and C++ backend's shared object in the right place
```bash
git clone 'https://github.com/MichalHe/amaya.git'
cd amaya
pip install -r requirements.txt
cp $AMAYA_MTBDD_DIR/build/amaya-mtbdd.so ./amaya
```

## Running amaya
```bash
./run-amaya.py --fast -O all get-sat <formula.smt2>
```
The `--fast` option enables the `C++` backend and turns on eager minimization.
The `-O all` option enables all formula optimizations, and also allows the solver
to use the derivative construction (dubbed internally as "lazy" backend).

## Creating an SMT-COMP submission archive
Python dependencies cannot be installed system-wide, and, therefore, one has to
set up a virtual environment, and install the dependencies there. Sylvan is also
installed system-wide. Therefore, the libsylvan.so object needs to be present in
the submitted archive, and `LD_LIBRARY_PATH` must be set accordingly when Amaya.
