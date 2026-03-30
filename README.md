# GitHub Nexus · Repo Manager Pro

A sleek, browser-based GitHub repository management tool featuring drag-and-drop ZIP deployments, branch management, and dual-mode synchronization strategies.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Platform](https://img.shields.io/badge/platform-Web-brightgreen.svg)

## Features

### 🔐 Secure Authentication
- GitHub Personal Access Token integration
- Secure token masking with visibility toggle
- Automatic user profile fetching

### 📁 Repository Management
- Browse all your repositories (public & private)
- Real-time search and filtering
- Create new repositories on-the-fly
- Repository visibility indicators

### 🌿 Branch Operations
- Switch between existing branches
- Create new branches from any base
- Visual branch selection interface

### 📦 Advanced Deployment

#### Full Sync (Mirror Mode)
- **Complete repository mirroring** - Makes target branch identical to ZIP contents
- Automatically deletes files/folders not present in the ZIP
- Updates existing files with new content
- ⚠️ *Destructive operation - use with caution*

#### Partial Update (Merge Mode)
- **Non-destructive updates** - Preserves existing repository structure
- Adds new files from ZIP
- Updates only files with matching names
- Safe for incremental deployments

### 🎯 User Experience
- **Drag & Drop** ZIP file upload (max 100MB)
- **Collapsible file tree** preview of archive contents
- Real-time deployment progress with detailed logs
- Glass-morphism UI with gradient accents
- Responsive design for desktop and mobile

## Quick Start

1. **Save the HTML file** to your local machine
2. **Open in any modern browser** (Chrome, Firefox, Safari, Edge)
3. **Get a GitHub Token**:
   - Go to GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)
   - Generate new token with `repo` and `workflow` scopes
4. **Paste token** and click "Connect"
5. **Select repository** and branch
6. **Choose deployment mode** (Full Sync or Partial Update)
7. **Drop your ZIP** and deploy!

## Usage Guide

### Authentication
Enter your GitHub Personal Access Token in the first step. The token is never stored permanently and only kept in memory during the session.

### Selecting Target
- Choose an existing repository from the grid
- Or click "New Repo" to create a fresh repository
- Select or create the target branch for deployment

### Deployment Modes

**When to use Full Sync:**
- Setting up a fresh project structure
- Want complete replacement of repository contents
- Cleaning up old files automatically

**When to use Partial Update:**
- Updating specific files without touching others
- Adding new components to existing project
- Safe production updates

### File Processing
- Supports standard ZIP archives
- Maximum file size: 100MB
- Preserves directory structure
- Binary-safe base64 encoding

## Technical Details

### Architecture
- **Frontend**: Vanilla HTML5, CSS3, JavaScript (ES6+)
- **Styling**: Tailwind CSS (via CDN)
- **Icons**: Lucide Icons
- **ZIP Processing**: JSZip library
- **API**: GitHub REST API v3

### API Endpoints Used
- `GET /user` - Authentication verification
- `GET /user/repos` - Repository listing
- `POST /user/repos` - Repository creation
- `GET /repos/{owner}/{repo}/branches` - Branch listing
- `POST /repos/{owner}/{repo}/git/refs` - Branch creation
- `GET /repos/{owner}/{repo}/git/trees/{ref}?recursive=1` - File tree fetching
- `PUT /repos/{owner}/{repo}/contents/{path}` - File upload/update
- `DELETE /repos/{owner}/{repo}/contents/{path}` - File deletion (Full Sync mode)

### Security Features
- Token input type="password" with visibility toggle
- No server-side storage - all operations client-side
- Direct GitHub API communication
- No external data persistence

## Browser Compatibility

| Browser | Version | Support |
|---------|---------|---------|
| Chrome | 90+ | ✅ Full |
| Firefox | 88+ | ✅ Full |
| Safari | 14+ | ✅ Full |
| Edge | 90+ | ✅ Full |

*Requires ES6 modules, Fetch API, and async/await support*

## Limitations

- **Rate Limiting**: Subject to GitHub API rate limits (5000 requests/hour for authenticated users)
- **File Size**: 100MB per ZIP file limit
- **No Git History**: Deployment creates new commits but doesn't preserve ZIP's internal git history
- **Single Branch**: Cannot deploy to multiple branches simultaneously

## Troubleshooting

**"Invalid token" error**
- Ensure your token has `repo` scope for private repositories
- Check that the token hasn't expired

**"Failed to delete" warnings in Full Sync**
- Some files may be protected or you may lack permissions
- Check repository branch protection rules

**Slow deployment**
- Large repositories with many files take time due to sequential API calls
- GitHub API has rate limiting - tool includes delays to respect limits
