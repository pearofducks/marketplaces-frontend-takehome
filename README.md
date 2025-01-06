# marketplace weather


## Implementation details

- The overall goal is to quickly get a prototype working for new weather functionality that could be added.
    - Your primary focus should be to make a UI that helps the user get the information they need quickly.
    - Your secondary focus is to utilize best practices in HTML and JS, so this prototype could be carried on to a full product if desired. You should ensure the app is accessible, but you should not worry about responsivity.
- A city and country should be accepted - and then present a 5-day forecast, as well as information on the next sunrise, sunset, moonrise, moonset, and moon phase.
    - All the APIs needed for this task are provided below.
- You should format the dates/times for the weather, ISO date formatting isn't very friendly for users. Likewise you should translate the moon phase into something understandable for a normal person.
- You will not be judged on 'design'. You do not need to worry about pretty colors, shadows, etc. You may need some CSS for layout (e.g. if you feel a sidebar or two-column layout is appropriate) or helping create a sense of hierarchy - but you do not (f.ex) need to worry about substituting stock fonts out for something else.
- You do not need to worry about error conditions from the API or presenting errors to the user

## Technical details

- You may use a popular framework such as React, Vue, Svelte - or you may also use plain JS if you feel it's appropriate.
    - [Vite](https://vite.dev/guide/#scaffolding-your-first-vite-project) is a good choice to quickly get a project bootstrapped for any of the above frameworks.
    - You should not use a meta-framework such as Next.js, Nuxt.js, or Sveltekit.
- You may *not* use any additional libraries other than one that simplifies working with `fetch`. [ky](https://github.com/sindresorhus/ky) is a fine choice if you don't have a preferred library.
    - This includes CSS libraries, any CSS should be standard CSS and not SCSS/SASS/Tailwind.
- All content should be on a single 'page' - you should not involve a router library or multiple pages
- The `dev` command in your project (e.g. `npm run dev`) *must* start your application in a useable form.
    - Vite comes with this command preconfigured.
- The city/country inputs mentioned above can be two input fields to simplify data handling
- If there are considerations you're aware of, but do not have time to implement - feel free to note these in your project's `README.md`

## APIs

### converting city/country to latitude/longitude

- Provider's docs: [Nominatim](https://nominatim.org/release-docs/develop/api/Search/)
- Example: For Oslo, Norway - `https://nominatim.openstreetmap.org/search?city=Oslo&country=Norway&format=json`

### weather data for a latitude and longitude

- Provider's docs: [met.no](https://api.met.no/weatherapi/locationforecast/2.0/documentation)
- Example: For Oslo, Norway - `https://api.met.no/weatherapi/locationforecast/2.0/compact?lat=59.913&lon=10.739`
- Notes:
    - You should send a maximum of 3 decimals for the `lat`/`lon` values

### sun and moon data for a latitude and longitude

- Provider's docs: [met.no](https://api.met.no/weatherapi/sunrise/3.0/documentation)
- Example: For Oslo, Norway - `https://api.met.no/weatherapi/sunrise/3.0/moon?lat=59.913&lon=10.739`
- Notes:
    - You should send a maximum of 3 decimals for the `lat`/`lon` values
 
#### sun

Relevant data provided by this endpoint:

```json
{
    "properties": {
        "solarmidnight": {
            "disc_centre_elevation": -52.59,
            "time": "2025-01-05T23:22+00:00",
            "visible": false
        },
        "solarnoon": {
            "disc_centre_elevation": 7.67,
            "time": "2025-01-06T11:23+00:00",
            "visible": true
        },
        "sunrise": {
            "azimuth": 137.43,
            "time": "2025-01-06T08:14+00:00"
        },
        "sunset": {
            "azimuth": 222.67,
            "time": "2025-01-06T14:31+00:00"
        }
    }
}
```

#### moon

```json
{
    "properties": {
        "high_moon": {
            "disc_centre_elevation": 35.37,
            "time": "2025-01-06T16:56+00:00",
            "visible": true
        },
        "low_moon": {
            "disc_centre_elevation": -28.33,
            "time": "2025-01-06T04:32+00:00",
            "visible": false
        },
        "moonphase": 76.61,
        "moonrise": {
            "azimuth": 81.82,
            "time": "2025-01-06T10:15+00:00"
        },
        "moonset": {
            "azimuth": null,
            "time": null
        }
    }
}
```
