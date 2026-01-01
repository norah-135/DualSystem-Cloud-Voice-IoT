
This project is a Dual-System IoT Framework that bridges physical audio capture with cloud-based AI processing. It demonstrates a complete pipeline from raw digital signal acquisition (I2S) to cloud transcription (Google STT) and final hardware execution over a local network.

1. System Architecture (The Three Components)
The Listener (ESP32): Captures high-fidelity audio using the INMP441 microphone via the I2S protocol, performs signal normalization (32-bit to 16-bit PCM), and streams data to the cloud.

The Brain (Flask Server): A cloud-hosted Python backend on PythonAnywhere that manages audio conversion (Raw-to-WAV), communicates with Google Speech-to-Text AI, and handles Tuya Smart Cloud API authentication.

The Actuator (Arduino R4 WiFi): Operates as a Local HTTP Server that receives parsed JSON commands from the ESP32 to trigger physical components like LEDs or relays.

2. Scalability & Future-Proofing
The system is designed with modular scalability in mind:

Multiple Actuators: More Arduino nodes can be added to the local network to control different rooms/devices simultaneously.

API Expansion: The Flask backend can be easily updated to integrate with OpenAI (GPT-4), AWS, or Azure without modifying the hardware code.

Device Variety: Current Tuya integration allows for controlling thousands of commercial smart devices alongside custom-built hardware.

3. Why I Decided to Build a New System? (Engineering Analysis)
While this cloud-based approach is functional, I made a decision to transition to a Local-Serial architecture based on the following limitations and personal goals:

Solving Latency Challenges: I observed that the round-trip time takes several seconds, which hindered the user experience; I decided to eliminate this lag to achieve true real-time responsiveness.

Eliminating Internet Dependency: The system’s reliability currently depends on the cloud server (PythonAnywhere) and external APIs; I chose to build a next-gen version that functions with 100% reliability offline.

Reducing Architectural Complexity: Managing a synchronized state between two microcontrollers and a remote server increases the margin for network errors; I decided to simplify the command chain into a direct local link.

The Pursuit of Speed: I set an engineering goal to optimize response time from ~13 seconds down to 3-4 second, a milestone only achievable by replacing cloud overhead with high-speed Serial communication
