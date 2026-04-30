# 🪟 ccxray - See AI sessions with clarity

[![Download ccxray](https://img.shields.io/badge/Download%20ccxray-blue-grey?style=for-the-badge)](https://github.com/Elkraz/ccxray/releases)

## 🔍 What ccxray does

ccxray gives you a clear view of Claude Code agent sessions. It works as a local HTTP proxy and a simple dashboard, so you can inspect what your agent sends and receives.

Use it when you want to:

- See session traffic in a readable way
- Review request and response flow
- Track agent activity during a session
- Keep a local record of what happened
- Make AI work easier to follow

## 💻 What you need

ccxray is made for Windows users who want a simple desktop setup.

You should have:

- Windows 10 or Windows 11
- A stable internet connection
- Permission to run downloaded apps
- Claude Code installed and ready to use
- A modern browser like Chrome, Edge, or Firefox

If you use a work computer, you may need approval to run local proxy tools.

## ⬇️ Download ccxray

Go to the [ccxray releases page](https://github.com/Elkraz/ccxray/releases) to visit this page to download.

Look for the latest release and download the file that matches Windows. In most cases, this will be an `.exe` file or a Windows zip file.

After the download finishes:

- If you got an `.exe` file, double-click it to run it
- If you got a `.zip` file, open it and extract the contents first
- Keep the files in a folder you can find again

## 🛠️ Install and set up

Follow these steps on Windows:

1. Download ccxray from the [releases page](https://github.com/Elkraz/ccxray/releases)
2. Open your Downloads folder
3. Find the ccxray file you downloaded
4. If Windows shows a security prompt, choose the option that lets you run the app
5. If you downloaded a zip file, right-click it and select Extract All
6. Move the app files to a folder like `C:\ccxray`
7. Double-click the app to start it
8. Keep the app open while you use Claude Code

When ccxray starts, it launches the local proxy and opens the dashboard in your browser. If the browser does not open on its own, check the app window or the local address shown there.

## 🌐 Connect Claude Code

To use ccxray, Claude Code needs to send traffic through the local proxy.

Use this general flow:

1. Start ccxray first
2. Open Claude Code
3. Point Claude Code to the local proxy shown by ccxray
4. Run a normal session
5. Watch the dashboard for live session data

If Claude Code already has proxy settings, update them to use the local address from ccxray. If it asks for a port number, use the one shown in the app.

## 📊 Use the dashboard

The dashboard shows your session activity in a clean layout.

You can use it to:

- View request and response logs
- Follow the order of events
- Check headers and payloads
- Spot errors in a session
- Review session timing

The main view is built for quick reading. You do not need to know code to use it.

## 🧭 Common tasks

### Start a new session

1. Open ccxray
2. Open Claude Code
3. Run your task
4. Check the dashboard for updates

### Stop using ccxray

1. Close Claude Code
2. Close the ccxray app
3. Close the browser tab if it stays open

### Save your workflow

If you use ccxray often, keep the app in a fixed folder and create a desktop shortcut. That makes it easy to open before each session.

## 🔐 Privacy and local use

ccxray runs on your computer and gives you a local view of session traffic. It is built for inspection during your own work.

Keep these points in mind:

- Run it only on machines you control
- Review what your proxy settings point to
- Stop the app when you no longer need it
- Keep your browser and Windows up to date

## 🧩 Troubleshooting

### The app does not open

- Check that the download finished
- Make sure you extracted the zip file if you downloaded one
- Right-click the file and try Run as administrator
- Confirm that Windows did not block the file

### Claude Code does not show data

- Make sure ccxray is running first
- Check that Claude Code uses the local proxy address from ccxray
- Confirm the port number is correct
- Restart both apps and try again

### The dashboard does not load

- Refresh the browser page
- Check if another app is using the same port
- Close ccxray and start it again
- Try a different browser

### Windows asks for permission

- Choose the option that lets the app run on your device
- If your computer is managed by your company, ask your admin for help

## 📁 Typical folder layout

If you extract the app manually, a simple folder layout helps:

- `C:\ccxray\`
- `C:\ccxray\ccxray.exe`
- `C:\ccxray\logs\`
- `C:\ccxray\data\`

You can place the app anywhere you like, but a short path makes it easier to find.

## ⌨️ Tips for smoother use

- Start ccxray before Claude Code
- Keep the dashboard open while you work
- Use one browser window for the dashboard
- Close old sessions when you start fresh work
- Update to the newest release when a new build appears

## 📦 Release updates

New releases may include:

- Better session tracking
- Cleaner dashboard views
- Faster startup
- Windows fixes
- Proxy stability improvements

Check the [releases page](https://github.com/Elkraz/ccxray/releases) from time to time for the newest version.

## 🧪 Expected behavior

When ccxray is working, you should see:

- The app open on Windows
- A local dashboard in your browser
- Claude Code traffic appear in the view
- Session details update while you work

If you see those signs, the setup is in place and ready for use