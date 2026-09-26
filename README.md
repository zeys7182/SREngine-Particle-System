# SREngine Particle System

A modular C++ particle system implemented as part of **SREngine**.

The system was developed as an engine-level feature rather than a standalone effect. It covers particle simulation, emission, shape-based spawning, lifetime-driven parameters and GPU-based rendering, with the parameters exposed through the engine's editor/property system.

## Overview

The system separates particle generation, simulation and rendering into independent modules.

A particle is represented by runtime state including:

* position and direction
* velocity
* lifetime
* size
* color
* rotation and rotation speed

Particle parameters can be configured through the engine's property system, allowing effects to be adjusted without modifying the simulation code.

## Core Systems

### Particle Simulation

The update pipeline handles:

* velocity-based movement
* gravity
* external forces
* lifetime management
* size interpolation over lifetime
* color interpolation over lifetime
* rotation and angular velocity
* particle creation and removal

Particle state is updated every frame and synchronized with the rendering data when required.

### Emission

The emission system supports both continuous and event-based particle generation.

* Rate over Time
* Duration
* Looping
* Bursts
* Burst timing and count

This allows effects to combine continuous emission with controlled one-shot events.

### Emission Shapes

Particle spawn positions can be generated from different geometric regions:

* Point
* Sphere
* Box
* Cone

Shape parameters are exposed through the engine's property system.

### Randomized Parameters

Particle initialization supports configurable parameter ranges, allowing properties such as lifetime, speed, size and other initial values to vary between particles.

This provides procedural variation without requiring separate particle configurations.

## Rendering

Two particle rendering modes are supported.

### Billboard Particles

Camera-facing quads are generated for traditional sprite-based particles.

Particle size and color are passed to the rendering pipeline as per-particle data.

### Mesh Particles

Particles can also be represented by 3D meshes.

Mesh geometry is stored separately from particle instance data, allowing the same geometry to be rendered across many particles using GPU instancing.

This separates static mesh data from frequently changing per-particle state.



## Editor Integration

The particle system is integrated with the engine's reflection/property infrastructure.

Simulation and emission parameters can therefore be modified directly through the editor:



This includes parameters such as lifetime, speed, size, color, forces, rotation, emission rate, bursts and shape configuration.

## Architecture

The implementation is organized around several responsibilities:

```text
Particle System
├── Particle Data
├── Main / Simulation Module
├── Emission Module
│   └── Burst
├── Shape Module
│   ├── Point
│   ├── Sphere
│   ├── Box
│   └── Cone
└── Rendering
    ├── Billboard
    └── Mesh + GPU Instancing
```

The separation allows emission, simulation and rendering behavior to evolve independently.

## Screenshots

### Overview



### Emission Shapes



### Emission



## Engineering Focus

The main focus of the implementation was not a single visual effect, but building a reusable engine subsystem that can support different particle behaviors and rendering modes.

Key areas of the implementation:

* C++ runtime simulation
* modular particle architecture
* configurable emission
* procedural spawn shapes
* lifetime-based interpolation
* runtime particle state management
* GPU rendering integration
* mesh instancing
* editor/property integration
* synchronization of simulation data with rendering resources

## My Contribution

Implemented the particle system functionality within SREngine, including the particle runtime, emission logic, spawn shapes, simulation parameters, lifetime-based behavior and rendering integration.

The system was developed as part of the existing SREngine codebase.

## Source

The production SREngine source code is not publicly available.

This repository presents the technical implementation and selected visual results as a portfolio case study.
