### [[EBS (Elastic Block Store)]]:

1. **Limited Storage:** Unlike EFS, EBS does not provide limitless or unlimited storage capacity.
2. **Availability Zone Bound:** EBS volumes have to be in the same availability zone as the EC2 instance they're attached to.
3. **Raw & Unformatted:** EBS comes in a raw and unformatted manner; you have to format it before use.
4. **Primary Storage:** Acts like primary memory to your machine and is usually faster in terms of accessibility.
5. **Use-Case:** Suitable for database applications or applications requiring high IOPS.

### [[EFS (Elastic File System)]]:

1. **Unlimited Storage:** EFS offers limitless storage scalability, in contrast to EBS.
2. **Region-Wide Availability:** Does not need to be in the same availability zone as your EC2 instance, just in the same AWS region.
3. **Pre-Formatted:** Unlike EBS, EFS is already formatted and ready for use.
4. **Secondary Storage:** Acts like a secondary storage option, offering huge storage capabilities but usually at slower access speeds compared to EBS.
5. **Use-Case:** Suitable for content management systems or any applications where large and shared storage space is needed.