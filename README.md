# DuoM

Cross-play Minecraft server core written in Rust (`src/lib.rs`) with Android JNI integration and automated GitHub Actions builds across four Android ABIs (`arm64-v8a`, `armeabi-v7a`, `x86`, and `x86_64`), alongside a standalone `trinitymax_server` binary.

## Current Status

* **Minimal Listener / Handshake Skeleton:** Currently implements initial connection/ping/handshake parsing rather than full gameplay, login, world generation, or chunk streaming.
* **Java TCP (`0.0.0.0:25565`):** Reads incoming TCP data, decodes VarInt packet length/ID and handshake protocol version, and logs whether the client hits the `1.18+` crypto path (`>= 757`) or the pre-`1.18` / `1.16` path (`< 757`).
* **Bedrock UDP (`0.0.0.0:19132`):** Listens for RakNet Unconnected Ping (`0x01`) packets and responds with a RakNet Pong (`0x1c`) and MOTD string.
* **Android JNI Bridge:** Exposes `Java_com_trinitymax_server_RustBridge_startServer` to start the Tokio runtime on a background thread.
* **Tunnel Loop:** Runs a periodic heartbeat task (`run_tunnel_client`) every 30 seconds.

## GitHub Actions Build (`build-apks`)

* Compiles `libtrinitymax.so` across `aarch64-linux-android`, `armv7-linux-androideabi`, `i686-linux-android`, and `x86_64-linux-android`.
* Builds the standalone `trinitymax_server` binary.
* Builds Android APKs via Gradle (`assembleDebug`) and stages artifacts into `dist/` (`trinitymax-apks`).
