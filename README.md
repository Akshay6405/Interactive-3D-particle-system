# Interactive 3D Particles with Hand Tracking

A real-time, browser-based visualizer that combines Three.js 3D rendering with Google MediaPipe computer vision. This project creates a field of thousands of floating particles that react physically to your hand movements via your webcam.

# 🌟 Features
Computer Vision Control: Uses the webcam to track your hand in real-time. No mouse or touch required.
High Performance: Renders 8,000+ individual particles using THREE.BufferGeometry for 60FPS performance on modern devices.
Physics Engine: Custom lightweight physics simulating repulsion forces, spring tension (return-to-home), friction, and sine-wave floating.
Procedural Assets: Textures are generated programmatically via HTML5 Canvas (no external image files required).
Zero Install: Runs entirely in the browser using ES Modules and CDNs.


# 🚀 Getting Started
Prerequisites
Because this project requires access to your Webcam, modern browsers (Chrome, Firefox, Safari) enforce security restrictions that prevent it from running directly from your hard drive (e.g., file:///C:/Users/...).
You must run this file through a local web server (localhost) or HTTPS.
Installation & Running
Download the Code:
Save the project code as index.html.
Start a Local Server:
Choose one of the following methods to run the file:
Method A: VS Code (Easiest)
Install the "Live Server" extension in VS Code.
Right-click index.html and select "Open with Live Server".
Method B: Python
Open your terminal/command prompt in the folder containing the file and run:
code
Bash
 Python 3
python -m http.server 8000
Then open http://localhost:8000 in your browser.
Method C: Node.js
code
Bash
npx http-server .
Allow Permissions:
When the page loads, your browser will ask for permission to use the Camera. Click Allow.


# 🎮 How to Interact
Wait for the text "System Active: Raise Hand" to appear.
Raise your hand in front of the camera.
A small red marker will appear, tracking your index finger.
Move your hand through the particle cloud to push the particles away.
Remove your hand from the frame, and the particles will slowly float back to their original positions.


# 🛠️ Configuration
You can tweak the behavior of the system by modifying the constants at the top of the script in index.html:
code

JavaScript
// Change the number of particles (Lower this if lagging)
const particleCount = 8000; 

// Change colors (Hex values)
const color1 = new THREE.Color(0x00ff88); // Start color
const color2 = new THREE.Color(0x0088ff); // End color

// Physics adjustments (Inside animate function)
// Increase 1500 to make the "push" stronger
const force = 1500 / (distSq + 1);


# 🧠 Technical Details
Initialization: The script sets up a Three.js scene and creates a buffer of positions/velocities.
Vision Loop: MediaPipe analyzes the video feed frame-by-frame. It extracts the X/Y coordinates of landmark #8 (Index Finger Tip).
Mapping: The 2D video coordinates (0.0 to 1.0) are mapped to the 3D world coordinates (approx -60 to +60).
Physics Loop:
Calculates distance between the finger target and every single particle.
Applies a repulsion vector if the particle is close.
Applies a spring force to pull the particle back to its origin.
Updates the GPU buffer.


# 📄 License
This project is open-source. Feel free to modify and use it for your own creative coding experiments.
Troubleshooting:
Black Screen? Ensure you allowed camera access.
Nothing happening? Check your browser console (F12) for errors. Ensure you are not opening the file via file://.
Laggy? Reduce particleCount to 4000 or 2000.