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

> [!CAUTION]
> For all `finn.no` endpoints, you should send a maximum of 3 decimals for the `lat` and `lon` query parameters.

### converting city/country to latitude/longitude

Example URL For Oslo, Norway: `https://nominatim.openstreetmap.org/search?city=Oslo&country=Norway&format=json`

<details><summary>Expand to see data returned</summary>

```json5
[
  {
    "place_id": 149918278,
    "osm_type": "relation",
    "osm_id": 406091,
    "lat": "59.9133301",
    "lon": "10.7389701",
    "class": "boundary",
    "type": "administrative",
    "place_rank": 12,
    "importance": 0.762636026573792,
    "addresstype": "county",
    "name": "Oslo",
    "display_name": "Oslo, Norway",
    "boundingbox": [
      "59.8093113",
      "60.1351064",
      "10.4891652",
      "10.9513894"
    ]
  },
  {
    "place_id": 151483229,
    "osm_type": "relation",
    "osm_id": 2775550,
    "lat": "59.97239745",
    "lon": "10.775729194051895",
    "class": "boundary",
    "type": "administrative",
    "place_rank": 14,
    "importance": 0.444716384691183,
    "addresstype": "municipality",
    "name": "Oslo",
    "display_name": "Oslo, Norway",
    "boundingbox": [
      "59.8093113",
      "60.1351064",
      "10.4891652",
      "10.9513894"
    ]
  }
]
```

</details>

### weather data for a latitude and longitude

Example URL for Oslo, Norway: `https://www.finn.no/pf/wx/compact?lat=59.913&lon=10.739`

<details><summary>Expand to see data returned</summary>

```json5
{
    "properties": {
        "meta": {
            "units": {
                "air_pressure_at_sea_level": "hPa",
                "air_temperature": "celsius",
                "cloud_area_fraction": "%",
                "precipitation_amount": "mm",
                "relative_humidity": "%",
                "wind_from_direction": "degrees",
                "wind_speed": "m/s"
            },
            "updated_at": "2025-01-06T08:26:24Z"
        },
        // only one typical object is shown in the 'timeseries' array, but there will be many
        "timeseries": [
            {
                "data": {
                    "instant": {
                        "details": {
                            "air_pressure_at_sea_level": 995.1,
                            "air_temperature": -4.5,
                            "cloud_area_fraction": 100.0,
                            "relative_humidity": 81.7,
                            "wind_from_direction": 50.4,
                            "wind_speed": 7.0
                        }
                    },
                    // optional field
                    "next_12_hours": {
                        "details": {},
                        "summary": {
                            "symbol_code": "snow"
                        }
                    },
                    // optional field
                    "next_1_hours": {
                        "details": {
                            "precipitation_amount": 0.4
                        },
                        "summary": {
                            "symbol_code": "snow"
                        }
                    },
                    // optional field
                    "next_6_hours": {
                        "details": {
                            "precipitation_amount": 4.4
                        },
                        "summary": {
                            "symbol_code": "snow"
                        }
                    }
                },
                "time": "2025-01-06T09:00:00Z"
            }
        ]
    }
}
```

</details>

### solar data for a latitude and longitude

Example URL for Oslo, Norway: `https://www.finn.no/pf/wx/sunmoon/sun?lat=59.913&lon=10.739`

<details><summary>Expand to see data returned</summary>

```json5
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

</details>

### lunar data for a latitude and longitude

- Example for Oslo, Norway - `https://www.finn.no/pf/wx/sunmoon/moon?lat=59.913&lon=10.739`

<details><summary>Expand to see data returned</summary>

```json5
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

</details>
