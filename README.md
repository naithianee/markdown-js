# scraper ![npm version](https://img.shields.io/npm/v/music-review-scraper.svg) ![downloads](https://img.shields.io/npm/dm/music-review-scraper.svg) ![build status](https://github.com/music-tools/review-scraper/workflows/CI/badge.svg)

Scrape music review data from popular music publication websites. Extract album reviews, track ratings, and reissue coverage with structured data output.

## Installation

```bash
npm install music-review-scraper
# or
yarn add music-review-scraper
```

## Quick Start

```javascript
const musicScraper = require('music-review-scraper');

// Get latest highly-rated albums
musicScraper.getTopRatedAlbums()
    .then(albums => {
        albums.forEach(album => {
            console.log(`${album.title} - ${album.artist} (${album.rating}/10)`);
        });
    })
    .catch(error => {
        console.error('Failed to fetch album data:', error);
    });
```

## API Methods

### getTopRatedAlbums()
Retrieves recently reviewed albums with high scores.

**Returns:** Promise resolving to array of album objects
```javascript
{
    title: "Album Name",
    artist: "Artist Name", 
    rating: 8.7,
    reviewDate: "2024-01-15",
    genre: ["Electronic", "Experimental"],
    reviewExcerpt: "Compelling description...",
    coverArt: "https://example.com/cover.jpg"
}
```

### getFeaturedTracks()
Fetches currently featured tracks and singles.

**Returns:** Promise resolving to array of track objects  
```javascript
{
    title: "Track Title",
    artist: "Artist Name",
    album: "Source Album",
    duration: "3:45",
    releaseDate: "2024-01-10",
    audioPreview: "https://example.com/preview.mp3"
}
```

### getReissueReviews()
Gets reviews for recently reissued albums and special editions.

**Returns:** Promise resolving to array of reissue objects
```javascript
{
    originalRelease: "1998",
    reissueDate: "2024-01-20",
    format: ["Vinyl", "Digital"],
    bonusContent: ["Remastered", "Bonus Tracks"],
    label: "Record Label"
}
```

## Advanced Usage

### Error Handling
```javascript
musicScraper.getTopRatedAlbums()
    .then(data => processAlbums(data))
    .catch(error => {
        if (error.statusCode === 404) {
            console.log('Review page structure changed');
        } else if (error.statusCode === 429) {
            console.log('Rate limit exceeded - try again later');
        }
    });
```

### Custom Configuration
```javascript
const scraper = require('music-review-scraper').create({
    timeout: 10000,
    userAgent: 'MyMusicApp/1.0',
    maxRetries: 3
});
```

## Data Sources
Aggregates reviews from multiple established music publications. Includes both mainstream and independent coverage across various genres.

## Testing
Run the test suite to verify functionality:
```bash
npm test
# or
yarn test
```

## Rate Limiting
Be respectful to source websites. Implement caching and avoid excessive requests. Recommended minimum 5 seconds between batches.

## License
MIT License - see LICENSE file for complete terms.
