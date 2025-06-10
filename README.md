# YouTube Clone

A responsive YouTube clone web application built with HTML, CSS, and JavaScript that uses the YouTube Data API to fetch and display videos.

## Features

### Core Features
- **Homepage Dashboard**: Responsive grid layout displaying popular videos
- **Search Functionality**: Search for videos using YouTube Data API
- **Navigation Bar**: Fixed navigation with logo, search bar, and menu links
- **Responsive Design**: Works on desktop and mobile devices
- **Video Player**: Modal video player using YouTube iframes

### Bonus Features
- **Search Suggestions**: Real-time search suggestions with 300ms debouncing
- **Throttling**: Scroll and resize event throttling (250ms)

## Technologies Used
- HTML5
- CSS3 (Flexbox, Grid, Media Queries)
- JavaScript (ES6+, Async/Await)
- YouTube Data API v3
- Google Queries API for search suggestions

## Setup Instructions

### Prerequisites
- A YouTube Data API key from Google Developer Console
- A web server (for CORS compliance)

### Running Locally

1. **Clone the repository**
   ```bash
   git clone <your-repo-url>
   cd youtube-clone
   ```

2. **Get YouTube API Key**
   - Visit [Google Developer Console](https://console.cloud.google.com/)
   - Create a new project or select existing one
   - Enable YouTube Data API v3
   - Generate an API key
   - Replace the API key in `youtube_fixed.html`:
     ```javascript
     const API_KEY = 'YOUR_API_KEY_HERE';
     ```

3. **Start a local server**
   
   Using Node.js:
   ```bash
   npx http-server -p 8000
   ```
   
   Using Python:
   ```bash
   python -m http.server 8000
   ```

4. **Open in browser**
   ```
   http://localhost:8000/youtube_fixed.html
   ```

## API Implementation

### YouTube Data API Integration
- **Popular Videos**: Fetches trending videos using `/videos` endpoint with `chart=mostPopular`
- **Search**: Uses `/search` endpoint with user queries
- **Error Handling**: Comprehensive error handling for API failures
- **Rate Limiting**: Proper API usage to avoid quota issues

### Search Suggestions
- Uses Google Queries API: `https://suggestqueries.google.com/complete/search?client=youtube&ds=yt&q=${query}`
- Implements JSONP parsing for cross-origin requests

## Debouncing and Throttling Implementation

### Debouncing (Search Suggestions)
```javascript
// 300ms debouncing for search suggestions
searchTimeout = setTimeout(async () => {
    const suggestions = await fetchSearchSuggestions(query);
    displaySuggestions(suggestions);
}, 300);
```

### Throttling (Scroll/Resize Events)
```javascript
// 250ms throttling implementation
function throttle(func, limit) {
    let inThrottle;
    return function() {
        if (!inThrottle) {
            func.apply(this, arguments);
            inThrottle = true;
            setTimeout(() => inThrottle = false, limit);
        }
    };
}
```

## File Structure
```
├── youtube_fixed.html          # Main application file
├── youtube.html               # Original file (with issues)
└── README.md                  # This file
```

## Browser Compatibility
- Chrome (recommended)
- Firefox
- Safari
- Edge

## Notes
- Requires internet connection for API calls
- Some features may be limited by YouTube API quotas
- Search suggestions may be blocked by CORS in some environments

## Live Demo
[Deployed Link Here] - Replace with your actual deployment URL

## API Key Security
⚠️ **Important**: In production, never expose API keys in client-side code. Use environment variables and a backend proxy for secure API calls.
