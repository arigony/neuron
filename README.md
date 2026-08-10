# NeuroAR — H01 neuron in the hand

NeuroAR is a browser-based educational WebAR experience that places the repository's `neuron1.glb` model over the user's palm using webcam hand tracking.

## Current prototype

This branch contains the first AR prototype. It intentionally preserves `neuron1.glb` as the scientific morphology supplied in this repository and changes only its runtime transform (position, orientation and scale) for visualization.

### What works in v0.1

- loads the existing `neuron1.glb` without remeshing or replacing its geometry;
- interactive 3D gallery with Three.js;
- WebAR camera mode over HTTPS;
- MediaPipe HandLandmarker tracking;
- real palm-position anchoring rather than a fixed center-screen anchor;
- smoothed hand-following position, orientation and scale;
- thumb/index pinch contributes to model scale;
- front/rear camera switch;
- responsive mobile interface;
- H01 scientific context and source links;
- connection/synapse panel using `20240521-synapses.jpg` with attribution.

## Scientific accuracy decision

The current version **does not paint synthetic synapse dots onto `neuron1.glb`**. The H01 release provides synapse point annotations and incoming excitatory/inhibitory synapse meshes, but a neuron-specific 3D overlay should only be added after the H01 synapse coordinates corresponding to this same segment are extracted and transformed with exactly the same spatial transform used to produce the GLB.

This is deliberate: visual effect should not be mistaken for measured connectivity.

## Scientific basis

Primary paper:

> Shapson-Coe A, Januszewski M, Berger DR, et al. A petavoxel fragment of human cerebral cortex reconstructed at nanoscale resolution. Science. 2024;384(6696):eadk4858. doi:10.1126/science.adk4858

Key H01 resources:

- Science DOI: https://doi.org/10.1126/science.adk4858
- H01 released data: https://h01-release.storage.googleapis.com/data.html
- Google Research Neural Mapping datasets: https://sites.research.google/gr/neural-mapping/datasets/
- NIH Research Matters: https://www.nih.gov/news-events/nih-research-matters/study-reveals-unseen-details-human-brain-structure
- EurekAlert / AAAS release: https://www.eurekalert.org/news-releases/1043546

The 2024 reconstruction reports roughly 1 mm³ of human temporal cortex, about 57,000 cells, about 150 million synapses and 1.4 petabytes of imaging data. The tissue was surgically removed to gain access to an underlying epileptic focus.

## Image attribution

`20240521-synapses.jpg` is used as scientific connectivity context.

Credit shown in the interface:

> Google Research & Lichtman Lab, Harvard University; rendering by D. Berger, Harvard. Image disseminated by NIH Research Matters.

## H01 data licensing

The H01 Released Data page states that released datasets are licensed under Creative Commons Attribution 4.0 (CC BY 4.0).

## Technology

- HTML5 / CSS3 / JavaScript
- Three.js 0.160.0
- GLTFLoader
- OrbitControls
- MediaPipe Tasks Vision / HandLandmarker 0.10.34
- GitHub Pages-compatible static deployment

## Usage

GitHub Pages or another HTTPS static server is required for camera access.

1. Open the page on a phone or webcam-enabled computer.
2. Let `neuron1.glb` load.
3. Tap **Iniciar experiência AR**.
4. Grant camera permission.
5. Open your palm in front of the camera.
6. Move and tilt your hand; the neuron follows the palm.
7. Bring thumb and index finger closer/farther to alter scale.
8. Use **Conexões H01** to view the scientific connectivity context and references.

Append `?debug` to the URL to display hand landmarks for development.

## Next scientific step

Extract neuron-specific H01 synapse coordinates for the same segment used in `neuron1.glb`, validate coordinate transforms, and export a lightweight browser asset such as `synapses.json` or a compact binary point cloud. Only then should excitatory/inhibitory synapses be rendered directly around the AR neuron.
