# Group Evaluation of Cocco
This report is a result of the work between Eden Garza, Akeem Olawoyin, Eugene Lin, and Haolin Zhang. 

Below is the original README in the project repo.

# Group15 Cocco

## Build

The environment is built by a docker image. Before building up the environment, you may need to set up the environement variable to acquire the right docker image. If you are using x86 CPU (Intel, AMD) please type the following commend in the terminal to set up the environment variable.
```shell=
export DOCKER_ARCH=amd64
```
ARM CPU
```shell=
export DOCKER_ARCH=arm64
```

After setting the environment variable, type the following commend in the terminal to open the jupyter lab server.
```shell=
docker-compose up
```

Open the terminal in the jupyter notebook and type the following commend to install the additional packages:

```shell=
python3 -m pip install -r requirements.txt
```

## Execute

The algorithms are written in the `/util` directory.

```shell=
cd /util/
python3 graph.py
```

## Project Description

This project is our implementation of [Cocco](https://arxiv.org/abs/2402.00629), a hardware mapping co-exploration framework. Cocco treats neural netowrks as DAGs, where each node in the DAG is a layer of the network. By paritioning the DAG into subgraphs and using an efficient memory mapping algorithm that is compatible with any subgraph, Cocco maximizes memory reuse, reducing energy costs and memory bandwidth requirements. The framework achieves this by using a genetic algorithm to perform design space exploration (DSE), evaluating different graph partitioning schemes and hardware configurations. 

## Project Structure

Our project is organized as follows:
 - `README.md`: This file.
 - `requirements.txt`: The required packages to run the project.
 - `docker-compose.yaml`: A Docker compose file used to create the Jupyter lab server. This creates an environment where we can invoke Timeloop to evaluate the performance of different subgraph partitioning schemes and hardware configurations.
 - `workspace`: A directory containing the configuration for the Jupyter lab server. Configurations include establishing command line prompt and setting the home directory.
 - `utils`: A directory containing our implementation code.
   - `components`: A directory containing yaml files that describe the hardware components we utilize in our simulated architecture. These files are used by Timeloop to estimate energy costs based on our dataflow.
   - `arch.jinja2`: This file describes the Simba-like architecture we based our experiments on. 
   - `cnn_layers.py`: This file describes the architectures of the networks we ran our experiments on. These networks include VGG16 and ResNet152.
   - `graph.py`: This file contains the code we use to describe the networks in cnn_layers.py as DAGs. It includes the code to partition the network into subgraphs as well as the code to evaluate the cost of a graph by invoking Timeloop.
   - `mapping_template.yaml`: This file describes how data is mapped into the hardware accelerator.
   - `problem_template.yaml`: This file describes the shape of the problem, defining the dimensions of the networks we are optimizing.
   - `problem_translation.py`: This file allows us to modify problem_template and mapping_template based on which network we are working on and the configuration determined by the subgraph partitioning algorithm.
  
