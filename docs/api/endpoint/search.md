# ```GET``` /api/search.json
Usage of this endpoint is through URL Parameters.

### Parameters
Below you will find the needed information on how to use it, and what each parameter does.

***[Parameter table is incomplete -- work in progress]***

| Parameter |   Description | Example |
|---|---|---|
| q | Query for the content you want. Can be an artist name, playlist name, song, album etc. | ```/api/search.json?q=Panama``` |
| filter | ***Required*** - Filter for the search. [Click Here](#filters) for the filters | ```/api/search.json?q=Panama&filter=EgWKAQIIAWoKEAMQBBAKEAkQBQ%3D%3D``` |


This endpoint's response typically will look like this:

```ts
type Search = {
	contents: SongResult[] | PlaylistSearch[]
	continuation: NextContinuationData
}

interface NextContinuationData {
	continuation: string
	clickTrackingParams: string
}
```
The shape of contents will look like one of these, depending on what you are searching for:
```typescript
type SongResult = {
	album?: Album
	artistInfo?: ArtistInfo
	explicit?: string
	hash: string
	index?: number
	length?: string
	params?: string
	playlistId?: string
	title?: string
	thumbnails: [{ url: string }]
	type?: string
	videoId: string
}

interface PlaylistSearch {
	playlistId: string
	metaData?: string | string[]
	browseId?: string
	hash?: string
	title: string
	type?: string
	thumbnails?: Thumbnail[]
	continuation?: NextContinuationData
}
```

### <a name="filters">Filters</a>

```
Songs - "EgWKAQIIAWoKEAMQBBAKEAkQBQ%3D%3D"
Videos - "EgWKAQIQAWoKEAMQBBAKEAkQBQ%3D%3D"
Artists - "EgWKAQIgAWoKEAMQBBAKEAkQBQ%3D%3D"

Playlists:
		- All: "EgWKAQIoAWoKEAMQBBAKEAUQCQ%3D%3D"
		- Featured: "EgeKAQQoADgBagwQDhAKEAkQAxAEEAU%3D"
		- Community: "EgeKAQQoAEABagwQDhAKEAkQAxAEEAU%3D"
```
