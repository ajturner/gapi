## About

This document serves as a list of core specifications that need to be created. It will likely evolve quite a bit, as it has large implications for the overall architecture. And indeed creating the actual specifications should reflect back in how we think about what's next.

## Core

These should be a small number of core web specifications that would be a first entry point to any developer interested in geospatial. They should build on common core components, presenting a coherent easy to understand interface that is relatively easy to build.

**Features Server** - Return vector data as GeoJSON: geometry + fields. Cacheable (compatible with CDN's, easily queried for latest changes), self-describing (using OpenAPI to describe itself), and assuming 2D  flat feature structure (no nesting, no references). Extensible to enable alternate formats, notifications, transactions, statistics/aggregation, styling, generalization, etc. But those are independent specs. See https://www.planet.com/api-explorer/ for some inspiration.

**Pixel Server** - Return vector + raster data as images (png/jpeg - with extensions for jp2k/mrf/geotiff/multi-band data,etc). Core should be tile based (cacheable) in web mercator, time / depth aware, described by JSON. TileJSON is likely quite close. Extensions should allow for more flexibility - alternate projections, formats, more bands, time, no tiles, video frames, styling, etc. Assumes a grayer line between WMS and WCS concepts - both are pixels, coverage can just return more options - will need to figure out how exactly we divide up needed functionality, but likely shouldn't be completely separate services, but different sets of capabilities that are enabled.

## Core Components

These are a set of small API pieces that should be combined to build the core specs. But they should also be useful in their own right, for those who may not want the whole core interface but needs some geospatial pieces for their API.

**Capabilities** - How to negotiate between a client and server to obtain what operations it is capable of.

**Output formats** - How to request data in a different format.

**Core Filters** - numerical, time and string equals, comparison and range queries, plus BBOX geometry filtering.

**Advanced Filters** - More obscure geometry operations, like touches, contains, distance within, etc.

**Assets** - References to related data as a field from the core feature. Links to images, audio, video, etc.

**Reprojection** - How to respond to requests in different projections, and return data in a requested projection


## Profiles / extensions

These are extensions to the core that enable more specific functionality.

**Imagery Catalog Profile** - An API to search large imagery holdings, with set core shared schema. Likely quite similar to https://www.planet.com/api-explorer/ 

**Layer Catalog Profile** - CSW updated for REST+JSON, built on core feature server. The core metadata fields should be possible to add on to the core feature server.

**Domain Specific Profile** - Attempt to represent a domain specific GML profile as a feature server.