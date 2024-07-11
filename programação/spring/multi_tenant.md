Multi tenant permite que uma mesma aplicação possa utilizar diferentes bancos de dados ao mesmo tempo.

A classe `AbstractRoutingDataSource` determina o banco de dados para cada tenant

```java
public class MultitenantDataSource extends AbstractRoutingDataSource {

    @Override
    protected String determineCurrentLookupKey() {
        return TenantContext.getCurrentTenant();
    }
}
```

A classe `TenantContext` guarda o tenant atual para cada request.

```java
public class TenantContext {

    private static final ThreadLocal<String> CURRENT_TENANT = new ThreadLocal<>();

    public static String getCurrentTenant() {
        return CURRENT_TENANT.get();
    }

    public static void setCurrentTenant(String tenant) {
        CURRENT_TENANT.set(tenant);
    }
}
```