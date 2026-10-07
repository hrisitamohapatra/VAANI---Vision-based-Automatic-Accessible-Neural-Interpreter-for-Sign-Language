<p align="center">
</p>

<h1 align="center">VAANI</h1>
<p align="center"><b>Vi</b>sion-based <b>A</b>utomatic <b>A</b>ccessible <b>N</b>eural <b>I</b>nterpreter for Sign Language</p>

<p align="center">
  <img src="https://img.shields.io/badge/backend-Flask-0891B2" alt="Flask" />
  <img src="https://img.shields.io/badge/model-YOLO-4338CA" alt="YOLO" />
  <img src="https://img.shields.io/badge/frontend-React%20%2B%20Vite-4F46E5" alt="React + Vite" />

</p>

VAANI is a bidirectional Indian Sign Language interpreter. It turns hand
gestures captured from a webcam into text/speech in real time, and can also
go the other way — turning typed text into a sequence of fingerspelling
GIFs — so hearing-impaired and non-sign-language users can communicate
through a single interface.

---

## Preview

<table>
  <tr>
    <td width="50%">
      <img width="1600" height="717" alt="1000125041" src="https://github.com/user-attachments/assets/33fddcff-3b7d-4287-948f-79fc0929742a" alt="Home page screenshot placeholder" width="100%" />
      <p align="center"><sub>Home Page </sub></p>
    </td>
    <td width="50%">
      <img width="1600" height="750" alt="1000103624" src="https://github.com/user-attachments/assets/e3e0b2f6-33dd-47c0-8f5f-d2952181b0b9" />
      <p align="center"><sub> Word-to-Sign </sub></p>
    </td>
  </tr>
</table>


## Architecture

<p align="center">
 <img width="1916" height="736" alt="Screenshot 2026-08-31 153257" src="https://github.com/user-attachments/assets/eae890d4-addc-4f70-b9ee-b35dd6da6c7b" />
</p>

The frontend captures webcam frames, sends them to the Flask backend as a
base64 image (via `POST /predict` or the `/ws/predict` WebSocket), the YOLO
model classifies the hand sign, and the backend returns a label, confidence
score, and a matching fingerspelling GIF URL that the frontend renders back
to the user.

## Project Structure

```text
VAANI/
  backend/
    app.py
    requirements.txt
    model/
      best.pt                # add your trained model here
    utils/
      __init__.py
      prediction.py
    static/
      gifs/
        A.gif ... Z.gif      # add finger spelling GIFs
  frontend/
    package.json
    index.html
    vite.config.js
    src/
      main.jsx
      App.jsx
      api.js
      styles.css
      pages/
        HomePage.jsx
        LiveDetectionPage.jsx
  assets/
    banner.svg
    architecture.svg
    screenshot-home.svg
    screenshot-live-detection.svg
```
## Clone the repository
 
```bash
git clone https://github.com/theanamsaqib/VAANI---Vision-based-Automatic-Accessible-Neural-Interpreter-for-Sign-Language.git
```
```bash
cd VAANI---Vision-based-Automatic-Accessible-Neural-Interpreter-for-Sign-Language
```
## Backend Setup (Flask + YOLO)

1. Open terminal:
   ```bash
     cd backend
   ```
2. Install dependencies:
 ```bash
   pip install -r requirements.txt
```

3. Add model file:
   - Place `best.pt` in `backend/model/best.pt`
4. Add GIF assets:
   - Put `A.gif` to `Z.gif` in `backend/static/gifs/`
5. Run:
  ```bash
   python app.py
```

Backend runs at `http://localhost:5000`

## Frontend Setup (React + Vite)

1. Open terminal:
  ```bash
cd frontend
```
2. Install dependencies:
  ```
npm install
```
3. Run:
   ```bash
   npm run dev
   ```

Frontend runs at `http://localhost:5173`

## API

- `POST /predict`
  - Body JSON:
    - `{ "image": "<base64 data URL>" }`
  - Response:
    - `{ "label": "A", "confidence": 0.95, "gif_url": "/static/gifs/A.gif" }`

- `GET /health`
  - Returns server health and selected device.

- WebSocket (optional):
  - `ws://localhost:5000/ws/predict`
  - Send base64 image (data URL string), receive JSON response.

## Tech Stack

| Layer | Tools |
|---|---|
| Frontend | React, Vite, react-webcam, axios, react-router-dom |
| Backend | Flask, flask-cors, flask-sock |
| ML | Ultralytics YOLO, OpenCV, NumPy |
