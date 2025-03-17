## Regions

Physical location of co-located cluster of data centres (e.g. London).

Each group of logical data centres is an Availability Zone.

Most AWS services are region-scoped.

How to choose a region:
- Compliance - data governance and legal requirements (e.g. French data must be located in France)
- Proximity - close to customers for reduced latency
- Available services - not all services available in all regions.
- Pricing - can vary per region.


## Availability Zones

Each region consists of a minimum of 3 physically separate AZs (max is 6).

Sydney (ap-southeast-2) has 3 AZs:
- ap-southeast02a
- ap-southeast02b
- ap-southeast02c

Each AZ is one or more discrete data centres with redundant power, networking and connectivity

If ap-southeast02a goes down, ap-southeast02b should remain available.


## Edge Locations (Points of Presence)

AWS have 400+ points of presence (edge locations and regional caches) in 90+ cities across 40+ countries.
Content is delivered to user with low latency



Source: [Global Infrastructure Regions & AZs](https://aws.amazon.com/about-aws/global-infrastructure/regions_az/)

