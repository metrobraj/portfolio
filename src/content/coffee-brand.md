---
title: "tabCluster"
slug: "Distributed Computation"
client: "Distributed Computational Power Aid"
category: "Project"
services: "Decentralized Peer-to-Peer Local Computing Engine"
year: "2026"
featuredImage: "./images/coffee-brand/yeaaa.jpeg"
imageTwo: "./images/coffee-brand/clouds.jpeg"
imageThree: "./images/coffee-brand/3.jpg"
liveSite: "https://github.com/metrobraj/tabcluster-c2c-2026"
description: "tabCluster leverages browser-based P2P networking alongside local native thread execution, allowing developers, researchers, and students to run distributed batch math, 3D renders, and parallel data workloads without incurring centralized cloud infrastructure expenses."
isFeatured: false
isDraft: false
---

Key Features

Zero-Server Peer-to-Peer Mesh: Connect worker devices instantly via QR code or room code using WebRTC DataChannels. No intermediate servers store or process payload data.

Modular Task Splitter & Plugin Architecture: Custom job dispatcher system equipped with templates for different distributed computing patterns:

2D/3D Frame Splitter: Parallel visual rendering (Ray tracing, Fractals, Canvas tiles).

Parameter Grid Splitter: Multi-dimensional hyperparameter search and simulation scoring.

Data Stream Splitter: High-volume array processing and sequence evaluation (Collatz Conjecture, statistical sweeps).

Range/Key Splitter: Distributed cryptographic key search and parallel state space search.

Mini-Batch Splitter: Parallel mini-batch gradient calculations for machine learning workflows.

Native Worker Nodes (OS-Level Multi-Threading): An opt-in execution tier that bypasses browser sandbox limitations.
Native Python workers connect via WebSockets to execute unthrottled, multi-threaded CPU tasks at native speed.

GPU Hardware Acceleration (Experimental): Experimental WebGPU/WebGL acceleration pipelines for matrix-heavy node tasks.

Blender Distributed Render Engine (Experimental): Offload 3D Blender frame chunk rendering across connected cluster nodes(Incomplete).

Fault Tolerance & Heartbeat Recovery: Automatic 3-second heartbeat pipeline. Disconnected worker tasks are detected and automatically re-queued to active cluster nodes without data loss.

How It Works Under the Hood

under the hood, we got

P2P Mesh Setup & Signaling

The Host (Master Node) opens a room and registers its peer ID with a lightweight PeerJS signaling server.

Worker nodes join via QR code or direct URL link, establishing direct, encrypted WebRTC DataChannel connections to the host.

Once connected, signaling is bypassed completely—all network traffic moves directly peer-to-peer.

Workload Partitioning & Dispatch

The user inputs task configurations (JSON params) and worker execution logic (JavaScript/Python functions) into the Host UI.
The Host Dispatcher chunks the workload into discrete sub-tasks based on the selected Splitter Template.

Tasks are serialized and pushed over WebRTC DataChannels to connected worker nodes using zero-copy binary ArrayBuffers where applicable.
Background Multi-Thread Execution

Browser Workers: Compute runs inside dedicated HTML5 Web Workers isolated from the main UI thread. Workers query navigator.hardwareConcurrency to spawn threads matching the device's physical CPU cores.

Native Workers (Power Mode): Python worker processes connect to the host via a WebSocket bridge, executing unthrottled multi-threaded tasks directly on the host machine's OS threads.

Fault Tolerance & Heartbeat Liveness

The Host maintains a continuous 3-second heartbeat monitor across all active data channels.
If a worker node disconnects, freezes, or fails to respond within the liveness threshold, the Host Stale-Task Recovery Engine reclaims its active chunk and silently re-routes it to an available node.
Aggregation & Real-Time Telemetry

As workers complete chunks, raw results stream back to the Host.
The Host Aggregator reduces incoming chunk payloads in real time, updating the live canvas grid, TFLOPS estimation metrics, and job completion counters.

Tech Stack

Frontend & UI: HTML5, CSS3, HTML5 Canvas API

P2P Communication: WebRTC DataChannels, PeerJS (Client & Signaling)

Browser Compute: Native HTML5 Web Workers API, ArrayBuffer / Uint8ClampedArray binary transport

Native Compute: Python (Standard Library, WebSockets, multiprocessing)

Deployment: Hosted on Render

Hardware Interfacing: navigator.hardwareConcurrency

Quick Start

Browser Cluster Host (Master Node)

Open the hosted Render deployment link in your browser.
Share the generated Room URL or QR code with peer devices.

Browser Worker Nodes

Peer devices simply scan the host QR code or open the Room URL in any mobile or desktop browser.
Compute runs automatically in background Web Workers.

Native Worker Nodes (Power User Mode)

To connect a machine with full multi-threaded CPU access: python worker.py --room-id YOUR_ROOM_ID
