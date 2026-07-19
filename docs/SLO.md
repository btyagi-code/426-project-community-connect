# Service Level Objectives

## catalog-service (Bhawna's)

**Latency**: The GET /catalog/search endpoint must respond within 400ms at p95. If someone's standing at their laptop trying to decide whether to walk to a branch, a slow lookup basically defeats the purpose. They'll just leave without an answer.

**Reliability**: This endpoint must succeed at least 99% of the time. A failed lookup is annoying but not dangerous, worst case the patron just retries or calls the branch. So this one doesn't need to be super strict, just consistently up.

## holds-service

**Latency**: The place hold endpoint must respond within 500ms at p95, so patrons get an immediate confirmation of their spot in line during a popular release.

**Reliability**: The place hold endpoint must succeed at least 99.5% of the time, and needs to be exactly once. A duplicate request from a retry should not create two queue entries for the same patron, since that would unfairly bump them ahead or miscount real demand.

## lending-service

**Latency**: The checkout endpoint must respond within 600ms at p95, since patrons expect a digital loan to start right after they check it out.

**Reliability**: The checkout endpoint must succeed at least 99.9% of the time and must be exactly once. A retried checkout must not grant two licenses for a resource that only has one copy available. That would be an actual data integrity problem, not just an inconvenience.

## gateway-service (shared)

**Latency**: The cross branch availability endpoint must respond within 700ms at p95, since it has to call out to multiple branch catalogs before returning one combined result.

**Reliability**: This endpoint must succeed at least 99% of the time. If one branch is down, the gateway should still return results from the branches that are up instead of failing the whole request, since a full failure blocks patrons from getting any answer at all.

These are first pass commitments, not final engineering numbers. They'll shape our design decisions in later sprints and we'll measure against them starting in Sprint 3.