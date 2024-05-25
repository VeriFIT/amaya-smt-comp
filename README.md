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
apt install git cmake
```

### Installing Sylvan
```
git clone 'https://github.com/trolando/sylvan.git'
cd sylvan
git checkout v1.5.0
mkdir build
cd build
cmake -DBUILD_SHARED_LIBS=ON ..
make
make test
sudo make install
```

```bash
git clone https://github.com/MichalHe/amaya-mtbdd.git
cd amaya-mtbdd
make
```

```bash
git clone 'https://github.com/MichalHe/amaya.git'
cd amaya
pip install -r requirements.txt

