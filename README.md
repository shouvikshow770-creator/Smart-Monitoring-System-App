# FireGuard dashboard (Vercel-ready)

This is a static web app. It can be deployed on Vercel as-is and starts in **Demo Mode** with simulated values.

## Deploy
1. Upload this folder to a GitHub repository (all four files: `index.html`, `style.css`, `app.js`, `vercel.json`).
2. In Vercel, choose **Add New → Project**, import the GitHub repository, and deploy. No build command is needed; the project is static.
3. Open the deployment URL.

## Connect Firebase Realtime Database
1. Create a Firebase project, enable Realtime Database and register a Web App.
2. Copy the Web app config JSON (do not paste service-account credentials).
3. Open dashboard → **Setup**. Paste config JSON, optionally set the database URL and path (`fire_system/readings`), and save.
4. Dashboard expects the newest record to contain fields such as `flame` or `flameDetected`, `rainWet`, `rainRaw`, `mqRaw`/`gasAlarm`, `temperature1`, `humidity1`, `temperature2`, `humidity2`, `ds18b20_1`, `ds18b20_2`, and thermostat flags. Several common aliases are also supported.

**Important:** Your current ESP32 code runs its own Wi-Fi AP and serves `/api`; it does not publish readings to Firebase. To use live cloud data on Vercel, the ESP32 firmware must be adapted to connect to internet Wi-Fi and send readings to Firebase (or another cloud endpoint). Vercel cannot directly reach a phone/laptop's private ESP32 AP. Use restrictive Firebase database rules and never expose private service credentials in this frontend.

## Camera
Set the ESP32-CAM stream URL in Setup. A local IP stream may work only while the viewing device can reach the same network. Some browsers block HTTP camera streams from an HTTPS Vercel page (mixed content); in that case, use an HTTPS stream/proxy or open camera stream separately.
