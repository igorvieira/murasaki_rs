# murasaki_rs
> A TUI tool for resolving git conflicts and managing staging during merge or rebase operations.


[![CI](https://github.com/igorvieira/murasaki_rs/workflows/CI/badge.svg)](https://github.com/igorvieira/murasaki_rs/actions/workflows/ci.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Rust Version](https://img.shields.io/badge/rust-stable-brightgreen.svg)](https://www.rust-lang.org)


<img src="https://res.cloudinary.com/dje6m1lab/image/upload/v1769398314/ChatGPT_Image_Jan_26_2026_12_31_41_AM_f1xewn.png" width="700" height="430"  />

<img width="1004" height="672" alt="image" src="https://github.com/user-attachments/assets/35535246-0104-4d94-a4a6-78f8c1e52f64" />


## Installation

### Manual Installation

```bash
git clone https://github.com/igorvieira/murasaki_rs.git ~/.config/murasaki_rs
cd ~/.config/murasaki_rs
cargo install --path .
```

This will:
- Clone the repository to `~/.config/murasaki_rs`
- Build and install using `cargo install --path .`
- Install the `saki` binary to `~/.cargo/bin/`


## Usage

```bash
saki
```

The tool automatically detects the current git state:
- **Conflict Mode**: When there are merge/rebase conflicts to resolve
- **Staging Mode**: When there are no conflicts (stage, unstage, commit files)

## Interface

### Layout
- **Left Panel (30%)**: File list with status indicators
- **Right Panel (70%)**: Code view (conflicts) or diff view (staging)

### File List Sections (Staging Mode)
- **STAGED** (green): Files ready to commit
- **BOTH** (yellow): Files with staged and unstaged changes
- **UNSTAGED** (red): Working directory modifications

## Commands

### Navigation (Both Modes)
| Key | Action |
|-----|--------|
| `j/k` or `Up/Down` | Navigate files (file list) / Scroll (code view) |
| `Tab` | Switch focus between file list and code view |
| `Ctrl+d/Ctrl+u` | Scroll half page down/up |
| `?` | Show help modal |
| `q` | Quit |

### Staging Mode
| Key | Action |
|-----|--------|
| `a` | Stage selected file |
| `s` | Unstage selected file |
| `r` | Restore file (discard changes) |
| `c` | Open commit modal |

### Commit Modal
| Key | Action |
|-----|--------|
| `Enter` | Submit commit |
| `Esc` | Cancel and close modal |

### Conflict Resolution Mode
| Key | Action |
|-----|--------|
| `n/p` | Next/previous conflict |
| `c` | Accept Current (HEAD) |
| `i` | Accept Incoming |
| `b` | Accept Both |
| `u` | Undo resolution |

### After Resolving All Conflicts (Rebase)
| Key | Action |
|-----|--------|
| `c` | Continue rebase |
| `a` | Abort rebase |
| `s` | Skip commit |

## Workflow

### Conflict Resolution
1. Run `saki` in a repository with conflicts
2. Navigate files with `j/k`
3. Press `Tab` to enter code view
4. Navigate conflicts with `n/p`
5. Resolve each conflict: `c` (current), `i` (incoming), or `b` (both)
6. File is auto-saved when all conflicts are resolved
7. For rebase: choose continue/abort/skip

### Staging Workflow
1. Run `saki` in a repository without conflicts
2. Navigate files with `j/k`
3. Stage files with `a`, unstage with `s`
4. Press `c` to open commit modal
5. Type commit message and press `Enter`

## Features

### Unified Interface
- Single split-pane layout for both modes
- Context-aware keyboard shortcuts
- Seamless transition between conflict and staging modes

### Conflict Resolution
- Syntax highlighting for conflict regions
- Visual indicators for resolved/unresolved conflicts
- Color-coded conflict backgrounds:
  - Current (HEAD): Blue background
  - Incoming: Red background
  - Both: Purple background
- Auto-save after resolving all conflicts in a file

### Staging Mode
- Full git staging workflow
- Diff view with syntax highlighting
- Commit modal with error handling
- Files organized by status (staged/unstaged/both)

### Safety Features
- Atomic file writes to prevent data corruption
- Terminal cleanup on panic
- Input validation to prevent path traversal
- Version update checking on startup

## Structure

```
src/
├── domain/     # Data models (ConflictedFile, Resolution, GitOperation)
├── app/        # Application state (AppState, AppMode, ViewMode)
├── git/        # Git integration (status, staging, commits)
├── tui/        # User interface (split_pane, event handling)
└── version/    # Version checking
```

## Development

```bash
# Build
cargo build --release

# Tests (69 tests)
cargo test

# Lint
cargo clippy
```

## Documentation

- [CHANGELOG.md](CHANGELOG.md) - Version history and release notes
- [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md) - Architecture and design decisions
- [docs/CONTRIBUTING.md](docs/CONTRIBUTING.md) - Contributing guidelines
- [docs/IMPLEMENTATION.md](docs/IMPLEMENTATION.md) - Implementation details and fixes
- [docs/TESTING.md](docs/TESTING.md) - Testing guide and coverage

## Version

Current version: 0.1.1

See [CHANGELOG.md](CHANGELOG.md) for version history.

## License

MIT

## Contributing

See [docs/CONTRIBUTING.md](docs/CONTRIBUTING.md) for guidelines on how to contribute to this project.
