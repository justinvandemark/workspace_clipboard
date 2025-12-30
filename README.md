# 📋 Clipboard Sync

A browser-based clipboard sharing tool that enables instant text transfer between two devices using WebRTC peer-to-peer connection.

## Features

- **Instant Transfer**: Real-time text sharing via peer-to-peer WebRTC connection
- **No Account Required**: Simply generate a room code or join with an existing one
- **Ephemeral**: Text only exists while browsers are connected (nothing stored)
- **One-Click Copy**: Quickly copy any text block to your clipboard
- **Responsive Design**: Works on desktop and mobile browsers
- **Secure**: Unguessable room codes with cryptographic randomness (~1.1 trillion combinations)

## How to Use

### Creating a Room

1. Open the app in your browser on your local machine
2. Click **"Create Room"**
3. Copy the displayed room code (e.g., `h7k2-m9p4`)
4. Open the same app on your remote machine and click **"Join Room"**
5. Paste the room code and click **"Join"**
6. Once connected, start typing in the text area to send messages

### Joining an Existing Room

1. Get the room code from someone who created a room
2. Open the app in your browser
3. Click **"Join Room"**
4. Enter the room code in the input field (hyphens are auto-formatted)
5. Click **"Join"** to connect

### Copying Text

Each message has a **"Copy"** button that instantly copies the text to your clipboard. The button will show a checkmark briefly to confirm the copy was successful.

## Keyboard Shortcuts

- **Ctrl + Enter** (Windows) or **Cmd + Enter** (Mac): Send a message
- **Auto-Hyphen**: When joining, the room code hyphen is automatically added as you type

## Technical Details

### Architecture

- **Frontend**: Pure vanilla JavaScript (no build process required)
- **Peer-to-Peer**: Uses WebRTC data channels for direct browser-to-browser communication
- **Signaling**: PeerJS library provides free cloud signaling service
- **Clipboard**: Browser's native Clipboard API
- **Hosting**: GitHub Pages (static, free)

### Room Codes

- Format: 8 characters with hyphen (e.g., `abc-1234`)
- Character set: Lowercase letters and numbers (excludes ambiguous chars like 0/O, 1/l/i)
- Generated using `crypto.getRandomValues()` for cryptographic randomness
- Security: ~1.1 trillion possible combinations

### Browser Support

Works on:
- Chrome 76+
- Edge 79+
- Firefox 55+
- Safari 11+

## Deployment

### GitHub Pages (Recommended)

1. **Create a new repository** on GitHub (or use an existing one)
2. **Copy files** to the repo:
   ```bash
   git clone <your-repo-url>
   cd <repo-name>
   cp index.html README.md .
   git add .
   git commit -m "Add Clipboard Sync app"
   git push origin main
   ```

3. **Enable GitHub Pages**:
   - Go to repo Settings → Pages
   - Select "Deploy from a branch"
   - Choose branch: `main`, folder: `/ (root)`
   - Click Save

4. **Access your app** at: `https://<username>.github.io/<repo-name>`

### Alternative: Local Testing

To test locally before deploying:

```bash
# Start a simple HTTP server
python3 -m http.server 8000

# Then open http://localhost:8000 in your browser
```

## Limitations & Known Issues

- **Connection Requirement**: Both browsers must be open simultaneously (ephemeral connection)
- **Firewall**: Some corporate firewalls may block WebRTC. If connection fails, try:
  - Checking if WebRTC is allowed on your network
  - Using a VPN if allowed
  - Using a fallback relay server
- **Large Text**: Very large text blocks (>16KB) may need to be chunked
- **Persistent Storage**: No message history is saved (ephemeral by design)

## Fallback Option

If your corporate firewall blocks WebRTC, there's a server-relay alternative that uses WebSockets instead:

1. Deploy a relay server to a free service like Render.com
2. Replace the P2P connection with server-mediated message relay
3. Text flows through server (less privacy but works everywhere)

Contact for implementation of fallback option.

## Troubleshooting

**"Connection error" or "Failed to connect"**
- Verify the room code is correct
- Ensure both browsers have the same app open
- Check if WebRTC is blocked by firewall
- Try refreshing both pages

**Copy button not working**
- Browser may not have granted clipboard permission
- Try using native Ctrl+C / Cmd+C instead
- Clipboard API requires HTTPS (except localhost)

**Messages not appearing**
- Check connection status indicator (should be green/connected)
- Ensure other device is online and has app open
- Try closing and reopening the app

## Privacy & Security

- **Data**: Text only exists in browser memory while connected
- **Encryption**: WebRTC connections use DTLS/SRTP encryption by default
- **No Server Storage**: PeerJS only handles connection signaling, not your text
- **Room Codes**: Cryptographically random, not easy to guess or brute-force

## License

This is a personal utility app. Feel free to modify and use as needed.

---

**Questions or Issues?** Check the troubleshooting section or open an issue on GitHub.
