# Multi-AZ RDS Failover Operational Runbook

In the event of an availability zone impairment or scheduled maintenance failover:

1. **Verify Primary Health**: Check CloudWatch RDS metrics for `DatabaseConnections` and `ReadIOPS`.
2. **Initiate Controlled Reboot with Failover**:
   ```bash
   aws rds reboot-db-instance --db-instance-identifier nexus-prod-db --force-failover
   ```
3. **Monitor DNS Propagation**: AWS Route53/RDS endpoint CNAME updates within 45-60 seconds.
4. **Connection Pool Verification**: Application containers reconnect automatically via backoff retry strategy.
