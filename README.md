## Overview

A simple yet functional RTSS overlay that provides vital metrics ensuring proper insights during gameplay or stress tests.
The overlay uses joint data from RTSS and PresentMon built-in plugin that build the several metrics to monitor like CPU, GPU, and many more.

## Features
| Category | Data |
| - | - |
| GPU Driver | Edition/Version |
| CPU | Usage(%), Clock(MHz), Temp(C°), Power(W) |
| RAM (Total RAM) | Usage(GB) |
| GPU | Usage(%), Clock(MHz), Temp(C°), Power(W) |
| VRAM (Total VRAM) | Usage(GB), Clock(MHz), Temp(C°) |
| FPS (API) | Current, Average, 1%, 0.1% |
| Frametime | Graph |
| Presentation Model** | Hardware (Composed): Independent/Legacy flip; Composed: Copy |

### Overlay Previews
  <img src="https://raw.githubusercontent.com/zappthed/RTSS_metrics_overlay/refs/heads/main/Preview/RTSS_metrics_overlay_compact.png" style="max-height: 250px; width: auto;">
  <img src="https://raw.githubusercontent.com/zappthed/RTSS_metrics_overlay/refs/heads/main/Preview/RTSS_metrics_overlay_detailed.png" style="max-height: 500px; width: auto;">
  <img src="https://raw.githubusercontent.com/zappthed/RTSS_metrics_overlay/refs/heads/main/Preview/Zappthed_OVERLAY.png" style="max-height: 330px; width: auto;">

## Presentation Model**

### Flip (D3D11/12*)
  <img src="https://github.com/zappthed/RTSS_Metrics_Overlay/blob/main/Preview/presentation_model_d3d11-12_flip.png" style="max-height: 800px; width: auto;">
For a game using a Flip swap effect, there are various factors that determine which presentation model will be used:

- The requested display mode of the game.
    - (*) The Exclusive Fullscreen (FSE) section is not applicable to DirectX 12 games as its “exclusive mode” is merely an “emulated” mode where the Windows desktop temporarily changes resolution, refresh rate, and colorspace to the one requested by the game, but otherwise acts exactly like a regular borderless fullscreen window.
- Fullscreen Optimizations (FSO) toggle (only relevant for games running in Exclusive Fullscreen (FSE) mode).
- Whether Multi-Plane Overlay (MPO) are available on the hardware.
- And finally whether the swapchain and system fulfills the necessary requirements to engage a DirectFlip optimization:
    - DirectFlip: Your swapchain buffers match the screen dimensions, and your window client region covers the screen. Instead of using the DWM swapchain to display on the screen, the application swapchain is used.
    - DirectFlip with panel fitters (requires MPO): Your window client region covers the screen, and your swapchain buffers are within some hardware-dependent scaling factor (for example, 0.25x to 4x) of the screen. The GPU scanout hardware is used to scale your buffer while sending it to the display.
    - DirectFlip with multi-plane overlay (requires MPO): Your swapchain buffers are within some hardware-dependent scaling factor of your window dimensions. The DWM is able to reserve a dedicated hardware scanout plane for your application, which is then scanned out and potentially stretched to an alpha-blended sub-region of the screen.

