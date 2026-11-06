# AI Camera - Project Planning

browser application that uses the live camera to detect and track objects, with **no required paid API or backend**.

> **Status:** Planning only.
> No application code has been written yet.

## Start here

**[Read the beginner-friendly 10-page architecture guide (PDF)](docs/AI_Camera_Architecture_Beginners_Guide.pdf)**
The PDF includes:

- A big step-by-step architecture flowchart
- What the camera, frame scheduler, AI model, tracker, and overlay each do
- An example showing how a water bottle gets detected
- How camera permissions, Start/Stop, errors, and camera switching work
- Proposed React/TypeScript file structure
- Local setup commands and performance optimization
- Optional cloud API integration without exposing secret keys
- GitHub Pages publishing steps
- Six phases for building the app when you're ready
- A small glossary for beginners

## Proposed architecture

```text
Visitor opens the GitHub Pages website
                |
                v
Browser asks for camera permission
                |
                v
Camera shows a live video stream (on the visitor's device)
                |
                v
Frame scheduler chooses a new frame
                |
                v
Local AI model identifies supported objects
                |
                v
Tracker assigns temporary IDs
                |
                v
Canvas draws boxes, labels, and confidence scores
                |
                +----> repeat while camera is running

Optional, only on user request:
One snapshot -> protected serverless proxy -> cloud AI -> explanation
```

## Simple build order

1. Start/Stop camera and mobile layout
2. Local MediaPipe object detection
3. Draw bounding boxes, labels, and scores
4. Object tracking, camera switching, and error handling
5. Performance improvements and offline caching
6. GitHub Pages deployment and phone testing
7. Optional advanced models or cloud AI later

## Free-first technology choices

| Part | Recommended tool |
| --- | --- |
| User interface | React + TypeScript + Vite |
| Camera | Browser `getUserMedia()` |
| First detection model | MediaPipe EfficientDet-Lite0 |
| Drawing | HTML Canvas |
| Tracking | Class + IoU-based matching initially |
| Hosting | GitHub Pages |
| Optional advanced inference | ONNX Runtime Web |
| Optional scene explanation | Cloud AI behind a protected proxy |

## Important notes

- The main detector should run directly on the user's device. This avoids cloud inference fees and continuous camera uploads.
- A general object detector only recognizes its trained categories. It will not identify every unique product or brand.
- Browser JavaScript files are public. **Never commit API keys** or place secret keys in Vite environment variables that ship to the browser.
- Model weights and AI libraries have licenses; confirm them before commercial use.
- Browser support and performance vary. Test on real iPhone, Android, and desktop devices.
- Cloud AI free quotas may change; the core application should work without them.

## Official documentation to revisit

- [MediaPipe Object Detector for Web](https://ai.google.dev/edge/mediapipe/solutions/vision/object_detector/web_js)
- [MediaPipe Object Detection guide](https://ai.google.dev/edge/mediapipe/solutions/vision/object_detector)
- [MDN: getUserMedia](https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/getUserMedia)
- [ONNX Runtime Web](https://onnxruntime.ai/docs/get-started/with-javascript/web.html)
- [Vite deployment guide](https://vite.dev/guide/static-deploy.html)
- [GitHub Pages documentation](https://docs.github.com/en/pages)
- [Gemini API documentation](https://ai.google.dev/gemini-api/docs)

*Prepared November 2026. This repository is a plan to return to later.*
