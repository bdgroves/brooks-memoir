# whitney-portal-route.geojson

Waypoints and real trail geometry for the Mount Whitney Trail (east side,
Whitney Portal → summit). Built to accompany the *Two Hundred and Ninety
Miles, Then Straight Up* memoir page.

**Version 2** — replaces the earlier straight-segment approximation with the
actual GPS trace from a GaiaGPS "Mount Whitney" known-route GPX file.

## What's in the file

**5 point features** — the waypoints from the memoir's SVG map, now with
coordinates snapped to the real trail at each waypoint's known elevation:

| Waypoint | Elevation | Mile* | Camp night | Coordinates |
|---|---|---|---|---|
| Whitney Portal | 8,360 ft | 0.0 | 1 | 36.58707, -118.24014 |
| Outpost Camp | 10,365 ft | 3.2 | 3 (descent) | 36.57269, -118.25320 |
| Trail Camp | 12,000 ft | 5.8 | 2 | 36.56342, -118.27719 |
| Trail Crest | 13,600 ft | 9.0 | — | 36.57000, -118.29256 |
| Mt. Whitney Summit | 14,505 ft | 9.9 | — | 36.57848, -118.29247 |

*Mile numbers derived from the actual GPX trace (haversine distance along
the polyline). These differ slightly from the memoir SVG's numbers (Portal
0.0, Outpost 3.8, Trail Camp 6.0, Trail Crest 8.5, Summit 10.7) which are
the commonly-cited trail lengths. Both are "correct" — the GPX-derived
ones are what the imported trace actually measures. Choose whichever
you want to display; the mile-marker properties on each waypoint use the
GPX-derived numbers so they line up with the visible trail on the map.

**1 line feature** — the real Mount Whitney Trail geometry, 830 GPS
vertices from Whitney Portal all the way to the summit. Includes the 99
switchbacks between Trail Camp and Trail Crest as they actually curve. This
is the ascent portion only; the source GPX file was an out-and-back trace,
but the descent retraces the same trail so we kept just the ascent for
visual clarity.

## Source

- **Trail line:** GaiaGPS "Mount Whitney" known route (`Mount_Whitney.gpx`,
  91 KB, 1,660 total trkpts, ascent portion = first 830 points).
- **Waypoint identity/naming:** the memoir SVG map at
  `mt-whitney-1994.html`.
- **Coordinate cross-checks:** Wikipedia (Whitney Portal, Mt. Whitney
  summit), Mountain Project (Trail Crest), USGS.

## Load into GeoLibre

1. Open GeoLibre at [viewer.geolibre.app](https://viewer.geolibre.app) or
   the desktop app.
2. Add Data → Vector → GeoJSON → upload `whitney-portal-route.geojson`.
3. Both waypoints and the trail line load together. You may want to split
   them into two layers for independent styling — GeoLibre's attribute
   filter can separate by `geometry type` or `properties.type`.

## Style suggestions

**Waypoints** — the `marker_style` property suggests four visual tiers:

- **trailhead** — square marker, dark color (Portal — where it starts)
- **camp** — round marker, mid-color (Outpost, Trail Camp — overnights)
- **pass** — triangle or arrow, muted color (Trail Crest — the transition)
- **summit** — star or filled peak icon, gold or high-contrast (Mt.
  Whitney — the destination)

**Trail line** — a single solid color at ~3px works well. If you want to
highlight the 99 switchbacks specifically, they run roughly between
vertices ~460 and ~776 in the LineString coordinate array.

## For 3D terrain

GeoLibre's Cesium view should give you the mountain rising up. The trail
line rendered on 3D terrain is where this map really becomes storytelling
material — the switchbacks make visual sense once you can see the wall
they're climbing.

## Elevation vs. what's on the memoir page

Elevations in this file match the memoir's existing SVG map exactly (8,360
/ 10,365 / 12,000 / 13,600 / 14,505). The GPX file itself reports 14,465
ft at the summit — a 40 ft difference from the surveyed 14,505 ft that
appears on the memoir page. That difference is GaiaGPS DEM-sampled
elevation vs the official NAVD88 surveyed value, not a data problem. The
memoir number (14,505) is authoritative and stays.
