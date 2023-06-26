# AI Trip Planner API

The AI Trip Planner API is a RESTful API that allows you to plan a trip itinerary based on the desired location and number of days. It provides a convenient way to retrieve a detailed trip plan with activities for each day.

## API Endpoint

`GET https://ai-trip-planner.p.rapidapi.com/`

## Parameters

- `destination` (required): The location you want to plan your trip for.
- `days` (required): The number of days for the trip.

## Headers

The API requires the following headers to be included in the request:

- `X-RapidAPI-Key`: Your API key for authentication.
- `X-RapidAPI-Host`: The host for the RapidAPI endpoint.

## Response

The API response is in JSON format and contains the trip plan for the specified location and number of days. The response has the following structure:

```json
{
  "plan": [
    {
      "day": 1,
      "activities": [
        {
          "time": "9:00 AM",
          "description": "Arrive in Zanzibar and check-in to hotel"
        },
        ...
      ]
    },
    ...
  ]
}
```

Each day in the trip plan contains a day number and an array of activities. Each activity has a time and description.

## Example

Here is an example API call using cURL:

```bash
curl --location --request GET 'https://ai-trip-planner.p.rapidapi.com/?destination=Zanzibar&days=3' \
--header 'X-RapidAPI-Key: YOUR_API_KEY' \
--header 'X-RapidAPI-Host: ai-trip-planner.p.rapidapi.com'
```

The above request retrieves a trip plan for Zanzibar with a duration of 3 days.

## Conclusion

The AI Trip Planner API allows you to effortlessly plan your trip itinerary based on the desired location and number of days. Retrieve detailed trip plans with activities for each day, and make the most of your travel experience!
