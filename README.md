# alpha-ui

This repository contains the **UI components** for the Alpha project, organized into two main modules:

- **alpha-ui-main:** The main dashboard and UI (vanilla JS/HTML/CSS, with backend integration).
- **chatbot:** A React-based chatbot UI, embedded into the main dashboard.

---

## Repository Structure

```
alpha-ui/
├── alpha-ui-main/
│   ├── index.html
│   ├── main.[HASH].js
│   ├── style.css
│   ├── ChatWidget.css
│   ├── ...
├── chatbot/
│   ├── src/
│   ├── public/
│   ├── build/
│   ├── package.json
│   ├── ...
```

---

## Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/srinipalli/alpha-ui.git
cd alpha-ui
```

---

### 2. Install & Build the Chatbot (React) Module

This module is located in `alpha-ui/chatbot`. It is a standard React app bootstrapped with Create React App.

**Install dependencies:**

```bash
cd chatbot
npm install
```

**Build the production bundle:**

```bash
npm run build
```

- This will generate a `build/` directory containing the optimized static files.
- The main JavaScript file will have a unique hash in its filename (e.g., `main.52943a9f.js`).

---

### 3. Embed the Chatbot Build into the Main UI

- Copy the built `main.[HASH].js` file from `chatbot/build/static/js/` into the `alpha-ui-main/` directory.
- Update (or confirm) the `<script src="main.[HASH].js"></script>` reference in `alpha-ui-main/index.html` to match the new hash filename.
    - This has already been done if you see a file like `main.52943a9f.js` in `alpha-ui-main/` and a matching script tag in `index.html`[6].
- The chatbot React component will now be embedded and functional within the main UI.

---

### 4. Set Up and Run the Main UI

**Install dependencies for the main UI backend (if any):**

```bash
cd ../alpha-ui-main
npm install
```

> If there is no `npm start` or backend server for the main UI, you can serve the static files using a simple HTTP server or the provided Python script.

**Option 1: Use the provided Python server**

```bash
python static_server_with_proxy.py
```

- This script serves the static files and may proxy API requests as configured.

**Option 2: Use a simple Node.js static server**

```bash
npx serve .
```

or

```bash
python -m http.server 8080
```

**Access the app:**  
Open [http://localhost:8080](http://localhost:8080) (or the port specified in your server) in your browser.

---

## Development Workflow

- **For chatbot UI changes:**  
  - Edit code in `chatbot/src/`
  - Rebuild with `npm run build`
  - Copy the new `main.[HASH].js` to `alpha-ui-main/` and update the script tag in `index.html` if the hash changes.

- **For main UI changes:**  
  - Edit files in `alpha-ui-main/`
  - Restart your static server if needed.

---

## Notes

- **Hash file embedding:**  
  The React build process generates a hashed JS filename for cache busting. Always ensure the correct file is referenced in `index.html` after each build[6].

- **Backend Integration:**  
  The main UI integrates with backend services via API endpoints (see `api/` and `backend_fixed.py` in `alpha-ui-main/`). Adjust `.env` and configuration as needed.

- **Chatbot API:**  
  The chatbot React app communicates with its backend via APIs defined in `services/` or `services.zip` in the `chatbot` directory.

---

## Troubleshooting

- If the chatbot does not appear, check:
  - The script tag in `alpha-ui-main/index.html` matches the latest `main.[HASH].js` filename from the chatbot build.
  - All static assets are copied correctly.
  - The backend API endpoints are running and accessible.

---

## Scripts Reference

### alpha-ui-main (`package.json`)

- No custom start/build scripts; primarily serves static files and backend integration[4].

### chatbot (`package.json`)

- `npm start` – Run React app in development mode
- `npm run build` – Build production bundle (for embedding)
- `npm test` – Run tests

---

## Example: Embedding the Chatbot

1. Build the chatbot:
```bash
cd chatbot
npm run build
```

2. Find the new `main.[HASH].js` in `build/static/js/`
3. Copy it to `alpha-ui-main/`
4. Update (or confirm) the script tag in `alpha-ui-main/index.html`:
```html
<script src="main.[HASH].js"></script>
```

5. Serve `alpha-ui-main` as described above.

---

## License

_No license specified yet. Please add a LICENSE file to clarify usage rights._

---

## Contact

For issues or suggestions, open an issue in this repository.

---
