# Payara 5 vs Payara 6 — Key Differences

## Overview

| Feature | Payara 5 | Payara 6 |
|---|---|---|
| Jakarta EE specification | Jakarta EE 8 | Jakarta EE 10 |
| Minimum Java version | Java 8 | Java 11 |
| Namespace | `javax.*` | `jakarta.*` |
| MicroProfile version | MicroProfile 4.1 | MicroProfile 6.0 |
| GlassFish base | GlassFish 5 | GlassFish 7 |

## Jakarta EE Namespace Change

The most significant breaking change between the two versions is the namespace migration.
Payara 5 uses the legacy `javax.*` package namespace (Jakarta EE 8), while Payara 6 uses
the new `jakarta.*` namespace (Jakarta EE 10). All application code that imports `javax.*`
packages must be updated to use `jakarta.*` when migrating to Payara 6.

For example:

```java
// Payara 5 (javax namespace)
import javax.inject.Inject;
import javax.enterprise.context.RequestScoped;

// Payara 6 (jakarta namespace)
import jakarta.inject.Inject;
import jakarta.enterprise.context.RequestScoped;
```

## Java Version Requirements

- **Payara 5** supports Java 8, 11, and 17 (with caveats on 17).
- **Payara 6** requires Java 11 or later, and fully supports Java 17 and 21.

## MicroProfile

Payara 6 ships with MicroProfile 6.0, which brings updated versions of:

- MicroProfile Config
- MicroProfile Fault Tolerance
- MicroProfile Health
- MicroProfile JWT Authentication
- MicroProfile Metrics
- MicroProfile OpenAPI
- MicroProfile Rest Client
- MicroProfile Telemetry (new in MicroProfile 6, based on OpenTelemetry)

## CDI Changes

Payara 6 (Jakarta EE 10) requires explicit bean discovery mode. Applications that relied
on implicit bean discovery in Payara 5 may need to add or update their `beans.xml`:

```xml
<beans xmlns="https://jakarta.ee/xml/ns/jakartaee"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="https://jakarta.ee/xml/ns/jakartaee
         https://jakarta.ee/xml/ns/jakartaee/beans_4_0.xsd"
       version="4.0"
       bean-discovery-mode="all">
</beans>
```

## Summary

Migrating from Payara 5 to Payara 6 primarily requires:

1. Replacing all `javax.*` imports with `jakarta.*`
2. Upgrading to Java 11 or later
3. Updating any MicroProfile API usage to the newer versions
4. Reviewing CDI bean discovery configuration
