# JAX (javax.ws / jersey)

## CORS

### Response Handling

```Java
import javax.ws.rs.core.MediaType;
import javax.ws.rs.core.Response;
public class JaxUtils {
    public static Response.ResponseBuilder jsonResponse(Object entity) {
        return Response.ok(entity, MediaType.APPLICATION_JSON_TYPE);
    }
    public static Response postProcessResponse(Response.ResponseBuilder builder) {
        return builder
                .header("Access-Control-Allow-Origin", "*")
                .header("Access-Control-Allow-Credentials", "true")
                .header("Access-Control-Allow-Headers", "origin, content-type, accept, authorization")
                .header("Access-Control-Allow-Methods", "GET, POST, PUT, DELETE, OPTIONS, HEAD")
                .build();
    }
}
```

### Response filter

```Java
@Provider
public class CorsFilter implements ContainerResponseFilter {

    @Override
    public void filter(ContainerRequestContext requestContext,
                       ContainerResponseContext responseContext) throws IOException {
        responseContext.getHeaders().add(
                "Access-Control-Allow-Origin", "*");
        responseContext.getHeaders().add(
                "Access-Control-Allow-Credentials", "true");
        responseContext.getHeaders().add(
                "Access-Control-Allow-Headers",
                "origin, content-type, accept, authorization");
        responseContext.getHeaders().add(
                "Access-Control-Allow-Methods",
                "GET, POST, PUT, DELETE, OPTIONS, HEAD");
    }
}
```

## Tip:

To get HTTP context (Works with Spring Boot, too)

```Java
@Context HttpServletRequest req
```

## JAX vs WebMVC

| JAX RS                                                                                                | WebMVC                                                                                                        |
| ----------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| @Path("/")                                                                                            | @RequestMapping("/")                                                                                          |
| @GET @Path("users")                                                                                   | @Produces({MediaType.APPLICATION_JSON}) @GetMapping(path = "users", produces = "application/json")            |
| @QueryParam("s")                                                                                      | @RequestParam("s")                                                                                            |
| @PathParam("name")                                                                                    | @PathVariable("name")                                                                                         |
|@POST @Consumes(MediaType.APPLICATION_FORM_URLENCODED) @Produces("application/zip") @Path("generate")  | @PostMapping(path = "generate", consumes = "application/x-www-form-urlencoded", produces = "application/zip") |
