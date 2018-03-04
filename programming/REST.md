# Representative State Transfer (REST) Styles

<!-- Tocer[start]: Auto-generated, don't remove. -->

## Table of Contents

  - [Idempotent Requests](#idempotent-requests)
  - [Exponential Backoff](#exponential-backoff)

<!-- Tocer[finish]: Auto-generated, don't remove. -->

## Idempotent Requests

Consider supporting these requests for networks with high latency in `POST` requests. See Stripe's
[documentation](https://stripe.com/docs/api#idempotent_requests) for further details.

## Exponential Backoff

Build this into the client so that when the client attempts to retry a failed request, the retry
attempts slowly back off exponentially to give the server breathing room. This should include
randomness and jitter so that clients are retrying at different intervals. See Stripe's
[code](https://github.com/stripe/stripe-ruby/blob/1bb9ac48b916
b1c60591795cdb7ba6d18495e82d/lib/stripe/stripe_client.rb#L78-L92) for an example.
