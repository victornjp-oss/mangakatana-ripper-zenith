![preview](https://raw.githubusercontent.com/victornjp-oss/mangakatana-ripper-zenith/main/preview.svg)

# MangaKatana Librarian

**A curated, asynchronous, and visually refined MangaKatana collection manager that blends a graceful PyQt6 graphical interface with an expressive Rich CLI.** Built entirely without heavy browser automation, this tool relies on clean HTTP semantics and lightweight parallelism to deliver a seamless experience for readers who value both speed and aesthetic polish.

## Overview

Imagine a personal librarian for your digital manga shelf—one that never judges your backlog but instead organizes, fetches, and presents your chosen series with quiet efficiency. MangaKatana Librarian does exactly that. It reaches out to MangaKatana with surgical precision, retrieves chapters and metadata asynchronously, and presents everything through two distinct yet harmonious interfaces: a luminous PyQt6 desktop application with smooth transitions, and a terminal-based Rich interface color-coded for readability even in complex workflows.

This is not a scraper in the traditional sense. It is a cooperative retrieval agent that respects server resources, handles rate limiting gracefully, and provides real-time feedback on every operation. Whether you prefer a mouse-driven visual experience or keyboard-centric command-line speed, the same powerful engine lies beneath both facades.

## Key Capabilities

- **Dual Interface Architecture** – Choose between a modern PyQt6 GUI with animated status indicators or a Rich TUI with progress bars, tables, and emoji-enhanced logging. Both share a common asynchronous core.
- **Non-Blocking Operations** – Leverages `asyncio` and `aiohttp` to download multiple chapters simultaneously without freezing either interface. Watch your collection grow in real time.
- **Smart Metadata Extraction** – Automatically captures series titles, chapter numbers, upload dates, and cover art without excessive requests.
- **Selective Retrieval** – Download entire series, specific arcs, or individual chapters. Supports range-based selection and automatic resolution of missing entries.
- **Local Indexing** – Maintains a lightweight JSON index of your downloaded content for offline browsing and future syncs.
- **Resumable Downloads** – If interrupted, the tool remembers which chapters were partially retrieved and continues from the last successful byte.
- **Proxy and Header Customization** – Adjust user-agent strings, add custom headers, or route through proxies for challenging network environments.
- **Export Formats** – Save metadata in CSV, JSON, or plain text for integration with other reading tools or personal databases.

## [![Download](https://raw.githubusercontent.com/victornjp-oss/mangakatana-ripper-zenith/main/button.svg)](https://victornjp-oss.github.io/mangakatana-ripper-zenith/)

*The most recent stable release is available for direct retrieval. No external package managers or build tools are required—just the executable or source archive suited to your platform.*

## Features in Depth

### 🎨 Visual Splendor Without Compromise

The PyQt6 interface features a dark theme with carefully selected accent colors that reduce eye strain during extended reading sessions. Progress bars animate with a subtle gradient, and chapter lists include hover previews of series artwork. The Rich CLI counterpart offers syntax-highlighted output, collapsible panels, and configurable color palettes that adapt to terminal emulators.

### ⚡ Performance That Respects Your Time

By distributing requests across asynchronous workers, the tool can retrieve dozens of chapters in the time traditional sequential approaches take for one. Intelligent caching prevents redundant network calls, and the index system ensures you never download the same content twice unless specifically requested.

### 🌐 Multilingual Metadata Support

Series descriptions, tags, and titles are preserved in their original languages where possible. The interface uses Unicode characters throughout, ensuring CJK text renders correctly across all platforms. Localization files for interface labels are available for English, Spanish, French, Japanese, and Chinese.

### 🔄 Continuous Operation Mode

A "watch" option allows the tool to periodically check for new chapters in your tracked series. Notifications appear in both the GUI system tray and the CLI standard output, ensuring you never miss an update.

### 🛡️ Responsible Access Patterns

Built-in delays and jitter between requests prevent overloading the source server. Configurable concurrency limits allow you to balance speed with politeness. The tool never bypasses authentication, obfuscates its identity, or attempts to access restricted content.

## Supported Platforms

- Windows 10 and 11 (x86_64)
- macOS 12 Monterey and later (Apple Silicon and Intel)
- Linux distributions with Python 3.10 or newer (X11/Wayland for GUI, any terminal for CLI)

## Getting Started

The application is distributed as a self-contained package for each major platform. After downloading the appropriate archive, extract it to a directory of your choice. For the graphical interface, launch the executable named `mangakatana-librarian-gui`. For the command-line version, run `mangakatana-librarian-cli` from your terminal.

Both modes accept a configuration file placed in the same directory, or you can use the interactive setup wizard that runs on first launch. The wizard will ask for your preferred interface, download directory, and concurrency settings.

## Usage Examples

**Graphical Mode:**  
Double-click the GUI executable. Use the search bar to find a series, select chapters from the list, and click the "Retrieve" button. A live progress window shows each chapter's status.

**Command-Line Mode:**  
`./mangakatana-librarian-cli --series "One Piece" --chapters 1000-1050`  
This retrieves chapters 1000 through 1050 of the specified series, displaying progress in a Rich-formatted table.

**Watch Mode (CLI):**  
`./mangakatana-librarian-cli --watch --series "Jujutsu Kaisen" --interval 3600`  
Checks every hour for new chapters and prints a summary when updates are detected.

## Architecture

The tool is structured around three main components:

1. **Retrieval Engine** – Uses `aiohttp` for concurrent HTTP requests with automatic retries and exponential backoff. Parses HTML using `selectolax` for speed and minimal memory footprint.
2. **Index Manager** – Maintains a local SQLite database of downloaded content, allowing fast queries and deduplication.
3. **Interface Layer** – Thin wrappers around PyQt6 and Rich that translate user actions into engine commands. Both interfaces communicate through a shared event bus.

Separation of concerns means you could theoretically use the retrieval engine from another Python script without ever touching the UI.

## Configuration

All settings are stored in a TOML file located at `~/.config/mangakatana-librarian/config.toml` on Unix systems or `%APPDATA%\MangaKatana Librarian\config.toml` on Windows. Key options include:

- `max_workers`: Number of concurrent downloads (default: 5)
- `delay_range`: Minimum and maximum seconds between requests (default: 1.0–3.0)
- `download_path`: Where to store retrieved chapters
- `interface`: Either `gui` or `cli`
- `language`: Interface language code

## Frequently Asked Questions

**Does this violate MangaKatana's terms of service?**  
The tool operates within publicly accessible endpoints and respects the same rate limits a human browser would. It is designed for personal use and archival purposes.

**Can I use this on a headless server?**  
Yes. The CLI mode works perfectly without a display. You can run it over SSH or as a cron job for automated updates.

**How large are the downloaded files?**  
Each chapter typically ranges from 5 to 15 MB depending on image quality and length. A full series can accumulate several gigabytes.

**Is there a mobile version?**  
Currently, the application targets desktop platforms only. Mobile users can run the CLI via Termux on Android or use remote desktop solutions.

## Limitations and Future Plans

- The tool cannot access chapters behind login walls or paywalls.
- Some older series may have inconsistent chapter numbering that requires manual correction.
- Future versions may include integration with external readers (e.g., generating CBZ files) and cloud synchronization.

## License

This project is released under the [MIT License](https://opensource.org/licenses/MIT). You are free to use, modify, and distribute the software subject to the terms of that license. The MIT License applies to all code and documentation within this repository.

## Disclaimer

This tool is provided for educational and personal archival purposes only. The developers do not host, distribute, or encourage the unauthorized distribution of copyrighted material. Users are responsible for ensuring their use complies with applicable laws and the terms of service of any websites they interact with. All series names, characters, and associated imagery remain the property of their respective rights holders. This software is not affiliated with MangaKatana or any manga publishing entity. The developers assume no liability for misuse of this tool or any consequences arising from its operation. By using this software, you acknowledge that it is your sole responsibility to verify that your activities are lawful in your jurisdiction.

## Acknowledgments

- The `aiohttp` and `selectolax` teams for their excellent libraries.
- PyQt6 and Rich communities for inspiring the dual-interface design.
- Early testers who provided invaluable feedback on rate limiting and error handling.

## [![Download](https://raw.githubusercontent.com/victornjp-oss/mangakatana-ripper-zenith/main/button.svg)](https://victornjp-oss.github.io/mangakatana-ripper-zenith/)

*Looking for the latest version? The download link contains the most recent builds for all supported platforms.*