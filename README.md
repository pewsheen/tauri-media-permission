# How to test

- `pnpm install`
- `pnpm tauri build`
- Open the `media-permission.app` inside `src-tauri/target/release/bundle/macos/`
- Click `Start Capture` in the app window
- Should ask for permission for microphone and camera
- Quit app and restart, then click `Start Capture` again, should not ask for permission but the camera capture works
