## File Integrity & Intrusion Detection (AIDE)

The **File Integrity Operator (FIO)** ensures security compliance and system immutability. 

Left unconfigured, the default AIDE configuration flags legitimate, dynamic system activities as security breaches. As SREs, we maintain strict exclusion rules to filter out system "noise" (such as changing log offsets, container runtime state files, and ephemeral metrics) so that our security monitoring alerts only on genuinely malicious or unexpected system modifications.

### Applying File Integrity Custom Profiles
To apply the custom integrity profile with tailored SRE exclusions:

```bash
oc apply -f clusters/production/file-integrity-exclusions.yaml