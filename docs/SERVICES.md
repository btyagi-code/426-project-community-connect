Team target: 4 services (3 members + 1 shared).


catalog-service (Bhawna's): Handles book and digital resource search and availability lookups across branches. This is what a patron hits when they're checking if something is in stock and where.
holds-service: Manages hold requests and queue position for patrons waiting on an item that's currently checked out somewhere else.
lending-service: Manages digital resource checkouts, active loans, due dates, and returns.
gateway-service (shared): Routes incoming patron requests to the right branch or service and aggregates availability info across branches into one response.


This is our first pass based on the domain (catalog browsing, holds, digital lending, and cross branch coordination). Ownership may shift slightly and scope will get more specific as we learn more patterns in later sprints.