## API Overview
Collection of information for movies, tv-shows, actors. Includes youtube trailer url, awards, full biography, and many other usefull informations. This api provides complete and updated data for over 9 million titles ( movies, series and episodes) and 11 million actors / crew and cast members. Support developers: https://www.buymeacoffee.com/SAdrian13
## for version
version 1 (v1)
## Available Endpoints
### 1. Titles
- `/titles`  
  Returns a list of titles based on optional filters, sorting, or predefined lists.
  
- `/titles/{id}`  
  Returns detailed information for a specific title using its IMDb ID.

- `/titles/{id}/ratings`  
  Retrieves rating information for a title (rating average and vote count).

- `/x/titles-by-ids`  
  Returns multiple titles by sending a list of IMDb IDs.

### 2. Seasons and Episodes
- `/titles/series/{id}`  
  Returns all episodes in ascending order (episode ID, number, and season number).

- `/titles/seasons/{id}`  
  Returns only the number of seasons for a series.

- `/titles/series/{id}/{season}`  
  Returns all episode IDs within a specific season.

- `/titles/episode/{id}`  
  Returns detailed information about an episode.

### 3. Upcoming Titles
- `/titles/x/upcoming`  
  Returns movies or series scheduled for release.

### 4. Search
- `/titles/search/keyword/{keyword}` — Search using keywords.  
- `/titles/search/title/{title}` — Search using full or partial title names.  
- `/titles/search/akas/{aka}` — Search using alternate titles (AKAs).

### 5. Actors
- `/actors`  
  Returns actors list with limit and pagination options.

- `/actors/{id}`  
  Returns complete details about a specific actor.

### 6. Utilities
- `/title/utils/titleType` — Returns available title types.
- `/title/utils/genres` — Returns available genres.
- `/title/utils/lists` — Returns available movie/series list categories.

## Request and Response Format
### Request Format
- Requests are made through HTTPS endpoints.
- Query parameters are optional unless specified.
- Paths requiring IDs must use valid IMDb IDs (e.g., `tt1234567`).
- Queries can include filters such as genre, year, sorting, and predefined lists.

### Response Format
- All responses return an object containing a `results` property.
- Endpoints that use pagination also include `page`, `next`, and `entries`.
- Each `result` is structured based on the model (title, actor, rating, episode, etc.).
- 
```json
{
  "results": [
    {
      "id": "tt1375666",
      "titleText": "Inception",
      "genres": ["Action", "Sci-Fi"],
      "ratingsSummary": {
        "averageRating": 8.8,
        "numVotes": 2300000
      }
    }
  ],
  "page": 1,
  "next": 2,
  "entries": 5
}

## Authentication
To use the MoviesDatabase API, you must:
- Subscribe to the API on RapidAPI.
- Use your API key within the request headers.

Typical header usage:
- `X-RapidAPI-Key`: Your API key
- `X-RapidAPI-Host`: Hostname from the API documentation

Without valid authentication headers, requests will fail.

## Error Handling

The API commonly responds with errors for:
- Missing or invalid IMDb IDs in the path.
- Incorrect header authentication.
- Invalid query formatting.

Error messages may include:
- Unauthorized or invalid API key.
- Resource not found (`404`).
- Bad request due to illegal query format (`400`).

To handle errors correctly:
- Always verify the ID and query values before sending requests.
- Validate that headers include an active API key.
- Check error messages and avoid retry loops that exceed limits.

## Usage Limits and Best Practices

- The API may have rate limits depending on your RapidAPI subscription.
- Reduce unnecessary large responses by:
  - Using pagination (`limit`, `page`)
  - Filtering results with query parameters (e.g. `year`, `genre`, `sort`)
  - Specifying `info` fields only for needed data (e.g., `mini_info`, `rating`)

Best practice suggestions:
- Cache frequent requests locally.
- Request only the data fields your app displays.
- Handle network errors and retry responsibly.
