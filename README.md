# Standalone Zephyr application template

[![GitHub Build workflow status](https://github.com/kaizoku-oh/zephyr-app-workspace/workflows/Build/badge.svg)](https://github.com/kaizoku-oh/zephyr-app-workspace/actions/workflows/build.yaml)
[![GitHub release](https://img.shields.io/github/v/release/kaizoku-oh/zephyr-app-workspace)](https://github.com/kaizoku-oh/zephyr-app-workspace/releases)
[![GitHub issues](https://img.shields.io/github/issues/kaizoku-oh/zephyr-app-workspace)](https://github.com/kaizoku-oh/zephyr-app-workspace/issues)
![GitHub top language](https://img.shields.io/github/languages/top/kaizoku-oh/zephyr-app-workspace)
[![License](https://img.shields.io/github/license/kaizoku-oh/zephyr-app-workspace)](https://github.com/kaizoku-oh/zephyr-app-workspace/blob/main/LICENSE)

This repo can be used as a template and a playground for experimenting with a standalone Zephyr application.

## 🚀 Getting started

```bash
# Initialize workspace for the app (main branch)
$ west init -m https://github.com/kaizoku-oh/zephyr-app-workspace --mr main workspace
$ cd workspace

# Setup python virtual environment
$ export PIPENV_VENV_IN_PROJECT=1
$ mkdir .venv
$ touch Pipfile
$ pipenv shell
$ pip install -r deps/zephyr/scripts/requirements.txt

# Update Zephyr modules
(zephyr-app-workspace) $ west update

# Copy vscode workspace file from the app to the outer workspace directory
(zephyr-app-workspace) $ cp app/linux.code-workspace .

# Build the app
(zephyr-app-workspace) $ west build app -d app/build -b nucleo_f767zi

# Turn on compilation database
(zephyr-app-workspace) $ west config build.cmake-args -- -DCMAKE_EXPORT_COMPILE_COMMANDS=ON

# Retrieve `ZEPHYR_SDK_INSTALL_DIR`
(zephyr-app-workspace) $ cmake -P deps/zephyr/cmake/verify-toolchain.cmake

# Open vscode workspace
(zephyr-app-workspace) $ code zephyr-linux.code-workspace
```
Once vscode is open you can run your workspace tasks like the following

![image](https://github.com/kaizoku-oh/zephyr-app-workspace/assets/22129291/b1eca6ce-78d9-469e-8675-fe2e84a79f1e)

You can run the tasks in the following order Clean => Build => Erase => Flash

![image](https://github.com/kaizoku-oh/zephyr-app-workspace/assets/22129291/08cda574-0ea5-4c34-8598-d53e3c5c96de)

Once the app is flashed open a serial monitor like PuTTY and reset your board.

![image](https://github.com/kaizoku-oh/zephyr-app-workspace/assets/22129291/d1f073a3-197b-40f9-8e73-649a705cd287)

## 🔨 Build footprint for NUCLEO-F767ZI

| Memory region | Used Size   | Region Size | %age Used   |
| ------------- | ----------- | ----------- | ----------- |
| FLASH         | 186096 B    | 768 KB      | 23.66%      |
| RAM           | 65648  B    | 384 KB      | 16.70%      |
| QSPI          | 0     GB    | 256 MB      | 0.00%       |
| DTCM          | 12544  B    | 128 KB      | 9.57%       |
| IDT_LIST      | 0     GB    | 2   KB      | 0.00%       |

## ✅ ToDo

- [x] Blink board LED

- [x] Shell over UART

- [x] Fix vscode launch with cortex-debug

- [x] Add multithreading code

- [x] Add die temp sensor class

- [x] Add Github CI workflow

- [x] Add GitHub badges to readme

- [x] Enable C++20

- [x] Add lambda callback to Serial class

- [x] Add a simple Network manager class

- [x] Add NVS Storage class

- [x] Add HTTP client class

- [ ] Add an IoT app that reads die temperature, store it in NVS, retrieve it, format it then send it

- [ ] Run app in Renode

- [ ] Add configurable vscode tasks

- [x] Add vscode dev container environment

- [ ] Integrate Renode + robot in the CI workflow

- [ ] Build project with MCUBoot

- [ ] Solve the Shared Callback Registration problem in the Network class

- [ ] Add native simulator to vscode build task

- [ ] Add a script to download and setup the project (intellisense, structure, venv...)

- [ ] Add static code analysis with CodeChecker

- [ ] Add coverage testing with gcov

- [ ] Add unit tests using Ztest and run them using Twister

- [ ] Add integration tests

- [ ] Add HIL tests using GitHub local runner

- [ ] Add application events manager using zbus

- [ ] Automate updating the README.md Build footprint table automatically by running a post build

- [ ] Add debouncing mechanism to Button class

- [ ] Add OTA update example

- [ ] Add lambda callback to Button class

- [ ] Use the active object design pattern

- [ ] Use an event driven state machine using the SMF OS service and the message queue kernel object

- [ ] Add Local class for managing local time and geo-location

- [ ] Add MQTT client class

- [ ] Add TCP class

- [ ] Add an out-of-tree driver

## 💳 Credits
This project is generated from the [zephyr-vscode-example](https://github.com/beriberikix/zephyr-vscode-example) template by [Jonathan Beri](https://github.com/beriberikix).

It is following the [Golioth](https://github.com/golioth) recommended way to structure a zephyr app using manifest files, more on this in this [blog post](https://blog.golioth.io/improving-zephyr-project-structure-with-manifest-files/).
