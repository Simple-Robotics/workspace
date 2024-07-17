# Simple-Robotics Workspace

This project aggregates scripts and files to work on multiple Simple-Robotics projects at once.

## How to use it

To setup a workspace, follow these steps:

1. Populate the workspace
2. Configure CMakeLists.txt
3. Configure pixi.toml
4. Build the workspace

Projects inside a workspace are called **edited projects**.

### Populate the workspace

Use the following commands to clone projects you want to **edit**.

- eigenpy: `git clone https://github.com/stack-of-tasks/eigenpy.git --recursive -b topic/workspace`
- hpp-fcl: `git clone git@github.com:humanoid-path-planner/hpp-fcl.git --recursive -b topic/workspace`
- pinocchio: `git clone git@github.com:stack-of-tasks/pinocchio.git --recursive -b topic/workspace`
- pycppad: `git clone git@github.com:Simple-Robotics/pycppad.git --recursive -b topic/workspace`
- example-robot-data: `git clone git@github.com:Gepetto/example-robot-data.git --recursive -b topic/workspace`
- proxsuite: `git clone https://github.com/Simple-Robotics/proxsuite.git --recursive -b topic/workspace`
- proxsuite-nlp: `git clone https://github.com/Simple-Robotics/proxsuite-nlp.git --recursive -b topic/workspace`
- aligator: `git clone https://github.com/Simple-Robotics/aligator --recursive --recursive -b topic/workspace`

### Configure CMakeLists.txt

Uncomment the following lines corresponding to all **edited projects** in the [CMakeLists.txt](./CMakeLists.txt) file:

- eigenpy: `add_eigenpy()`
- hpp-fcl: `add_hpp_fcl()`
- pinocchio: `add_pinocchio()`
- pycppad: `add_pycppad()`
- example-robot-data: `add_example_robot_data()`
- proxsuite: `add_proxsuite()`
- proxsuite-nlp: `add_proxsuite_nlp()`
- aligator: `add_aligator()`

### Configure pixi.toml

This is the trickiest part.

The [pixi.toml](./pixi.toml) file contains the following environments:

- all: Allow to work on all projects at the same time
- eigenpy-standalone: Allow to work only on eigenpy
- hpp-fcl-standalone: Allow to work only on hpp-fcl
- pinocchio-standalone: Allow to work only on pinocchio
- pycppad-standalone: Allow to work only on pycppad
- proxsuite-standalone: Allow to work only on proxsuite
- proxsuite-nlp-standalone: Allow to work only on proxsuite-nlp
- aligator-standalone: Allow to work only on aligator
- loik-standalone: Allow to work only on loik

It also contains the following features:

- base: Dependencies used in a lot of projects
- eigenpy: eigenpy dependencies
- hpp-fcl: hpp-fcl dependencies without **editable projects**
- hpp-fcl-standalone: hpp-fcl **editable projects** dependencies
- pinocchio: pinocchio dependencies without **editable projects**
- pinocchio-standalone: pinocchio **editable projects** dependencies
- pycppad: pycppad dependencies without **editable projects**
- pycppad-standalone: pycppad **editable projects** dependencies
- proxsuite: proxsuite dependencies without **editable projects**
- proxsuite-nlp: proxsuite-nlp dependencies without **editable projects**
- proxsuite-nlp-standalone: proxsuite-nlp **editable projects** dependencies
- aligator: aligator dependencies without **editable projects**
- aligator-standalone: aligator **editable projects** dependencies
- loik: loik dependencies without **editable projects**
- loik-standalone: loik **editable projects** dependencies

You have to create an environment with all **edited projects** dependencies but without **edited projects** inside.
To achieve this, you can compose an environment with all defined features.

As an example, if you want to work on hpp-fcl and pinocchio you will need:

- All hpp-fcl dependencies: You can use the hpp-fcl and hpp-fcl-standalone feature
- pinocchio dependencies without hpp-fcl: You can use the pinocchio feature

You will have to add the following line in the [pixi.toml](./pixi.toml) environments section:

```yaml
my-env = { features = ["base", "hpp-fcl", "hpp-fcl-standalone", "pinocchio"] }
```

To help you build the right environment, here the **editable project** dependency graph:

- eigenpy: nothing
- hpp-fcl:
    - eigenpy
- pinocchio:
    - eigenpy
    - hpp-fcl
- pycppad:
    - eigenpy
- proxsuite: nothing
- proxsuite-nlp:
    - eigenpy
    - pinocchio
    - example-robot-data
    - proxsuite
- aligator:
    - eigenpy
    - pinocchio
    - example-robot-data
    - proxsuite-nlp
- loik:
    - pinocchio
    - example-robot-data

### Build the workspace

To build the workspace, open a pixi shell, then run CMake and make as usual:

```bash
pixi shell -e my-env
mkdir build
cd build
cmake ..
make
```

You can run all tests at once by running:

```bash
ctest
```

Or you can only select tests from a specific project:

```bash
ctest -R "pinocchio-.*"
```
