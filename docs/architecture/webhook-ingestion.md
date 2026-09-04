# Webhook Ingestion & Deduplication Architecture

Incoming webhooks follow an asynchronous ingestion pipeline:

1. **Edge Ingress**: ALB validates TLS and forwards to backend.
2. **Signature Verification**: HMAC-SHA256 signature is verified prior to JSON deserialization.
3. **Idempotency Check**: Event ID is recorded in Redis with a 72-hour TTL. Duplicate events receive instant HTTP 200 without reprocessing.
4. **Queue Dispatch**: Valid events are published to Amazon SQS FIFO queue for durable processing.
