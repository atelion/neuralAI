<div align="center">

# **NeuralAI** <!-- omit in toc -->
[![Discord Chat](https://img.shields.io/discord/308323056592486420.svg)](https://discord.gg/bittensor)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT) 

---

## The Incentivized Internet <!-- omit in toc -->

[Discord](https://discord.gg/bittensor) • [Network](https://taostats.io/) • [Research](https://bittensor.com/whitepaper)
</div>

---
- [Introduction](#introduction)
- [Key Features](#key-features)
- [Miner and Validator Functionality](#miner-and-validator-functionality)
  - [Miner](#miner)
  - [Validator](#validator)
- [Installation](#installation)
  - [Running Miners](#running-miners)
  - [Running Validators](#running-validators)
- [Benefit and use cases](#benefit-and-use-cases)
  - [Benefits](#benefits)
  - [Use Cases](#use-cases)
- [Upgrade](#upgrade)


## Introduction

NeuralAI is a cutting-edge subnet dedicated to the generation of 3D models using advanced neural network techniques. Our goal is to empower developers and artists with tools that simplify the creation of high-quality 3D assets for various applications, including gaming, virtual reality, and simulations.

## Key Features

- **High-Quality 3D Generation**: Generate realistic 3D models from simple inputs.
- **Customizable Parameters**: Adjust settings to fine-tune the output according to specific project needs.
- **Real-Time Rendering**: View generated models in real-time with minimal latency.
- **Cross-Platform Compatibility**: Easily integrate with popular game engines and 3D modeling software.

## Miner and Validator Functionality

### Miner
- Miners in the NeuralAI Subnet are responsible for powering the computational infrastructure that enables the 3D asset generation and processing capabilities.
- Generally, miners queue and when receive a request (the format will be text format) from validators, they produce 3d mesh object by contributing their computational resources.
- After producing a 3D mesh object, the object is sent to validators who assess and provide scores that evaluate the quality of the production and validators announce the scores to miners about their quality and speed of work.

### Validator
- Validators are responsible for verifying and validating miners’ work regarding the quantity of 3d mesh object within the network.
- First validators assign tasks to available miners by sending prompt made of text format.
- When receive the miner’s work, they render images in different axis from the response and validate the scores by comparing the similarity of the prompt and rendered images.
- Validators validate scores with the quality of work and execution time.
- After validating the scores, they set miners’ weights and send scores to miners so that miners are able to recognize their performance of models.

## Installation

### Running Miners
We recommend setup using Python>=3.10, PyTorch>=2.1.0, and CUDA>=12.1.

Download the source from the github
```commandline
git clone https://github.com/GoNeuralAI/neural-subnet/
cd neural-subnet
pip install -r requirements.txt
```

#### Generation endpoint with PM2
```commandline
cd generate
pip install -r requirements.txt
pm2 start serve.py --interpreter python3 --name {endpoint} -- configs/instant-mesh-large.yaml --export_texmap --axon.port {port}
```

#### Run Miner with PM2
```comandline
pm2 start "python3 neurons/miner.py
    --netuid {netuid}
    --wallet.name {wallet}
    --wallet.hotkey {hotkey}
    --axon.port {port}"
 --name miner
```

### Running Validators

#### Validation endpoint with PM2
```commandline
cd validation
pip install -r requirements.txt
pm2 start "serve.py --axon.port {port}"
```

#### Run Validator with PM@
```commandline
pm2 start "python3 neurons/validator.py
    --netuid {netuid}
    --wallet.name {wallet}
    --wallet.hotkey {hotkey}
    --axon.port {port}"
 --name validator
```

## Benefit and use cases
### Benefits
- Quality-Focused Approach
By prioritizing the quality of the generated 3D objects over the speed of generation, the subnet can ensure that the output meets the desired high standards.
This focus on quality helps to maintain the integrity and usability of the 3D assets, which is crucial for applications that require precise and visually appealing 3D content.
- Efficient Computational Resource Allocation
The 'Validator First' structure allows the validators to actively assign computational work to the miners, optimizing the utilization of available resources.
This approach can help avoid potential issues related to validator traffic and heavy computational workloads, ensuring a more stable and reliable operation of the subnet.
- Outlier Detection and Filtering
The use of Isolation Forest to detect and filter out outliers in the image-text similarity scores helps to improve the overall quality of the generated 3D objects.
By removing outliers, the subnet can focus on the most relevant and high-quality associations between the images and text prompts, leading to better 3D model generation.

### Use Cases
(Usecase part should be included in the subnet documentation in the subnet github repository.)
- 3D Asset Generation for Content Creation
The subnet can be used to generate high-quality 3D assets for various content creation applications, such as video games, virtual reality experiences, architectural visualizations, and product design.
The focus on quality ensures that the generated 3D models can be seamlessly integrated into these applications, providing realistic and visually appealing content.

- 3D Modeling Assistance for Designers and Creators
The subnet can be integrated into design tools and platforms, providing designers and creators with a powerful AI-driven 3D modeling assistance.
Users can leverage the text-to-3D capabilities to quickly generate 3D models based on their descriptive prompts, accelerating the content creation process.
- Educational and Training Applications
The subnet can be utilized in educational and training environments, where the generation of accurate 3D models can aid in visualization, simulation, and interactive learning experiences.
The high-quality 3D assets produced by the subnet can enhance the educational value and immersive nature of these applications.
- Prototyping and Visualization for Product Development
The subnet can be employed in product development workflows, enabling designers, engineers, and product teams to quickly generate 3D prototypes and visualizations based on their conceptual ideas.
This can streamline the iterative design process and facilitate more informed decision-making during the product development lifecycle.

By focusing on quality, efficient resource utilization, and outlier detection, the proposed subnet design can be a valuable asset in various industries and applications that require high-quality 3D content generation and modeling capabilities.


## Upgrade
- Version 1 focuses on validating the quality of miner responses in an acceptable duration. validators Validate miners with “Challenge” synapse only.

- Version 2 will extend to validate the miners’ generation capacity as well as quality. We will include additional synapses like “Discovery”, “Feedback”.
“Discovery” synapse will ask miners for their generation capacity which will incentivize miners include multi-GPUs to increase generation capacity. “Feedback” synapse will let miners get feedback from their generation results to further improve their generation results.

Further subnet roadmap should be discussed among the team
