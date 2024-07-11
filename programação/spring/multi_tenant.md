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

A classe `TenantFilter` é o filtro que irá resgatar o tenant de dentro do cabeçalho da requisição. É necessário definir no frontend um cabeçalho denominado "X-TenantID" para cada requisição.

```java
@Component
@Order(1)
class TenantFilter implements Filter {

    @Override
    public void doFilter(ServletRequest request, ServletResponse response,
      FilterChain chain) throws IOException, ServletException {

        HttpServletRequest req = (HttpServletRequest) request;
        String tenantName = req.getHeader("X-TenantID");
        TenantContext.setCurrentTenant(tenantName);

        try {
            chain.doFilter(request, response);
        } finally {
            TenantContext.setCurrentTenant("");
        }
    }
}
```


